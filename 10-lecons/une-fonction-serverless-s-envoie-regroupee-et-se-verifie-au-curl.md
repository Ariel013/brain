---
titre: Une fonction serverless s'envoie regroupée, et se vérifie au curl avant d'être annoncée
type: lecon
origine: FIBDA Bodybuilding — 2026-09-23 et 2026-09-26
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

**Seconde occurrence (FIBDA, 2026-09-26).** `vercel deploy --prebuilt` a rendu
le code 0, `/health` répondait `ok`… et la page servait **encore l'ancien
bundle** : la sortie du déploiement s'était arrêtée avant la mise en ligne. Le
curl de santé ne distingue pas l'ancienne version de la nouvelle. Règle
complétée : après chaque déploiement, lire dans la page servie le nom du
fichier `assets/index-<hash>.js` et le **comparer à celui de la construction
locale**, après quelques dizaines de secondes de propagation. Un code de retour
et une route qui répond ne sont pas une version en ligne.

**Troisième occurrence (CV interactif, 2026-10-25).** Un site Next.js sans
API : le déploiement Vercel « réussi », et **toutes les pages en 404**. Le
projet avait été créé sans framework détecté (« No framework detected ») et
servait le dossier brut. Correctif : `framework: "nextjs"` déclaré dans
`vercel.json`. Même règle, élargie : une mise en ligne se prouve par une
requête sur une page réelle, et non par le statut du déploiement. Le même
jour, une feuille de style périmée servie malgré un build réussi →
[[un-cache-de-build-restaure-peut-servir-l-ancienne-feuille-de-style]].

Voir [[regarder-l-application-fait-partie-de-la-recette]],
[[verifier-chaque-commit-du-decoupage]].
