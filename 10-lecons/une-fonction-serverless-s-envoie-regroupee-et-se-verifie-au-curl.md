---
titre: Une fonction serverless s'envoie regroupée, et se vérifie au curl avant d'être annoncée
type: lecon
origine: FIBDA Bodybuilding — 2026-09-23
tags: [vercel, serverless, deploiement, verification]
---

# Une fonction serverless s'envoie regroupée, et se vérifie au curl avant d'être annoncée

**Symptôme.** « ▲ Aliased » sur trois déploiements successifs, page d'accueil
et fichiers statiques servis en 0,25 s… et **chaque** route d'API en
`FUNCTION_INVOCATION_FAILED`, puis, une fois corrigé, en silence total (aucune
réponse jusqu'au délai de 60 s). Les logs n'étaient pas dans la sortie du
déploiement : il a fallu `vercel logs` pour lire `ERR_MODULE_NOT_FOUND
/var/task/server/app`.

**Cause.** Trois faits distincts, tous invisibles à la construction :
1. la plateforme a déployé le fichier TypeScript de la fonction **en ESM sans
   regrouper ses imports relatifs** — `../server/app` n'existait pas dans le
   paquet ;
2. le gestionnaire renvoyait une `Response` web alors qu'il était appelé avec
   la signature Node `(req, res)` : rien n'écrivait jamais la réponse ;
3. un déploiement lancé depuis un sous-dossier a, un jour sur deux, envoyé le
   dépôt git entier et détecté un « service » Python à la racine.

**Règle.** Pour une API serverless : **regrouper soi-même** la fonction en un
fichier au build (esbuild), accepter **les deux signatures** de gestionnaire,
et déployer **le résultat construit localement** (`vercel build` puis `vercel
deploy --prebuilt`) plutôt que de laisser la plateforme détecter et
construire. Et un déploiement n'est « en ligne » qu'après un `curl` sur une
route d'API réelle (`/health`), pas sur la page d'accueil : les statiques
répondent même quand la fonction est morte.

Voir [[regarder-l-application-fait-partie-de-la-recette]],
[[verifier-chaque-commit-du-decoupage]].
