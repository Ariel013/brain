---
titre: Un test de route emprunte le chemin que l'écran emprunte réellement
type: lecon
origine: FIBDA Bodybuilding — 2026-09-23
tags: [tests, contrat-api, frontend, portage]
---

# Un test de route emprunte le chemin que l'écran emprunte réellement

**Symptôme.** Backend réécrit dans un autre langage « au même contrat d'API »,
frontend conservé tel quel, 64 tests serveur verts dont un parcours complet de
compétition. La restauration d'une sauvegarde était pourtant **impossible
depuis l'écran** : l'écran envoyait un fichier en `multipart/form-data`
(champ `file`, filtre `.zip`), le serveur lisait le corps brut en JSON. Le test
de restauration passait parce qu'il envoyait… du JSON brut. C'est l'agent qui
rédigeait le mode d'emploi, en lisant l'écran, qui a vu l'écart.

**Cause.** Le test a été écrit depuis le point de vue du serveur (« ma route
accepte ceci »), pas depuis celui du client existant (« l'écran envoie
cela »). Quand le frontend préexiste, le contrat n'est pas ce que le serveur
déclare : c'est **ce que le client envoie déjà**.

**Règle.** Pour chaque route consommée par un écran existant, le test
reproduit **l'appel tel que l'écran le construit** (méthode, encodage du corps,
noms de champs, en-têtes), en lisant le code du client avant d'écrire le test.
Corollaire : écrire le mode d'emploi en lisant l'écran est une revue de
contrat gratuite — la faire avant de déclarer le portage terminé.

Voir [[ce-que-l-ecran-promet-le-code-le-fait]],
[[regarder-l-application-fait-partie-de-la-recette]].
