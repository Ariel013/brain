---
titre: Un découpage en commits se vérifie, il ne se suppose pas
type: lecon
origine: Synoé — 2026-08-23 et 2026-08-24 · Strongman — 2026-09-16 et 2026-09-19 · Synoé — 2026-10-04
tags: [git, agents]
---

# Un découpage en commits se vérifie, il ne se suppose pas

**Symptôme.** Cinq commits découpés en **supposant** l'ordre de dépendance, avec
un message affirmant que « chaque commit compile ». C'était faux : un module
dépendait d'une API introduite au commit **suivant**. Le commit du milieu ne
compilait pas.

**Cause.** L'ordre de dépendance a été déduit de la lecture, pas mesuré.

**Règle.** Quand un lot est découpé, **vérifier chaque commit isolément** avant
de partager quoi que ce soit — la seule preuve est de le sortir seul et d'y
lancer typecheck et tests.

Et **ne jamais écrire dans un message de commit une propriété qu'on n'a pas
mesurée** : l'affirmation survit à l'erreur.

**Le geste qui rend ça quasi gratuit.** Un worktree détaché par commit, avec les
dépendances en lien symbolique : quelques minutes pour tout le lot, sans toucher
à l'arbre de travail ni au serveur de développement — qu'on ne fait jamais
changer de branche sous les pieds.

**Même règle, autre objet (Strongman, 2026-09-16).** Un rapport et le
`A-FAIRE.md` affirmaient qu'une variable d'environnement malformée bloquait
toute connexion, « en local comme en ligne ». Faux : la production répondait
en ordre. Le diagnostic venait du poste local, étendu à la production sans
l'interroger — alors qu'une requête suffisait. Un état de production s'affirme
après l'avoir interrogé, et l'affirmation **nomme l'environnement mesuré**.

**Un déploiement se prouve par un contenu, pas par son statut (Strongman,
2026-09-19).** Après un push, le statut du déploiement lu sur le commit disait
encore `pending` alors que la production servait déjà le nouveau build ; au
push précédent, il disait `success` et rien ne prouvait que l'alias de
production pointait dessus. Dans les deux sens, le statut parle du build, pas
de ce que l'adresse publique sert. La preuve directe : chercher sur une page
publique **une phrase qui n'existe que dans ce commit** — et vérifier que
l'ancienne a disparu. Quand le changement est derrière une connexion, le dire :
« déployé, non vu à l'écran ».

**Deux lots dans un même arbre, un fichier en commun (Synoé, 2026-10-04).** Le
second lot a été codé avant que le commit du premier soit validé, et les deux
touchaient le même fichier. Ce qui a rendu le découpage possible sans rien
réécrire : **figer le premier lot dans un patch (`git diff > lot.patch`) avant
d'écrire la première ligne du second**. Au moment de committer, les fichiers
propres à un lot se stagent nommément, les fichiers communs par
`git apply --cached --include=<fichier> lot.patch` — l'index reçoit l'état du
premier lot, l'arbre garde les deux. Puis le commit se vérifie seul dans un
worktree détaché, comme toujours. Sans le patch pris **avant**, il aurait fallu
démêler les deux lots à la main dans le fichier commun.

Voir aussi [[nommer-la-copie-visee]], [[ecrire-la-decision-avec-le-code]], [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]].
