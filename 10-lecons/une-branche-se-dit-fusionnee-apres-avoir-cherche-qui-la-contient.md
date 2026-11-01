---
titre: Une branche se dit fusionnée après avoir cherché qui la contient
type: lecon
origine: Kalybris (rangement de la machine) — 2026-11-01
tags: [git, worktree, agents, menage]
---

# Une branche se dit fusionnée après avoir cherché qui la contient

**Symptôme.** Pendant un ménage du disque, 10 worktrees d'agents de Kalybris
(3 Go) ont été déclarés « non fusionnés, du travail en cours, de 65 à 101
commits hors de `dev` ». Recommandation donnée : ne pas y toucher. Vérification
faite à la demande suivante : les 10 branches étaient **entièrement contenues**
dans la branche de sprint courante, sans un seul commit propre. Elles étaient
supprimables depuis le début.

**Cause.** La question posée à git était « fusionnée dans `dev` ? »
(`git branch --merged dev`). Or le travail des agents remonte d'abord dans la
branche de sprint, qui n'est pas encore remontée dans `dev`. Une réponse
« non » à cette question-là ne dit rien de l'endroit où le travail se trouve.

**Règle.** Avant de qualifier une branche de « non fusionnée », chercher **qui
la contient** : `git branch --contains <branche>`, et le nombre de commits
propres contre la branche qui l'a reçue (`git rev-list --count <receveuse>..<branche>`,
`git cherry` pour les commits réécrits). Une branche contenue ailleurs, sans
commit propre et sans fichier modifié dans son worktree, se retire avec
`git worktree remove` puis `git branch -d` (qui refuse si quelque chose se
perdrait).

**Corollaire.** Les worktrees d'agents ne se nettoient pas seuls : après
fusion d'un lot, les retirer dans la même session, sinon ils s'accumulent
(3 Go ici, dont la moitié verrouillés).

Voir [[un-worktree-d-agent-part-de-main-pas-de-la-branche-courante]],
[[nommer-la-copie-visee]], [[lire-la-donnee-avant-l-hypothese]].
