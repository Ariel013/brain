---
titre: Un découpage en commits se vérifie, il ne se suppose pas
type: lecon
origine: Synoé — 2026-08-23 et 2026-08-24
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

Voir aussi [[nommer-la-copie-visee]], [[ecrire-la-decision-avec-le-code]].
