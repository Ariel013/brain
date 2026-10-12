---
titre: Un worktree d'agent part de `main`, pas de la branche courante
type: lecon
origine: Kalybris — 2026-10-08 (nuit)
tags: [git, agents, worktree, brief]
---

# Un worktree d'agent part de `main`, pas de la branche courante

**Symptôme.** Quatre agents lancés en worktree isolé depuis une branche de
sprint. Trois d'entre eux ouvrent leur rapport par « le worktree avait été
créé sur `main`, les fichiers cités dans la tâche n'y existaient pas, je
l'ai réaligné ». Le quatrième — un front — a travaillé et committé sur
`main` sans s'en rendre compte, parce que sa tâche ne citait aucun fichier
qui manquait ; il a fallu l'interrompre pour un rebase.

**Cause.** L'isolation crée le worktree depuis la branche par défaut du
dépôt, pas depuis `HEAD`. Un brief qui dit « branche dérivée de X » décrit
une intention ; rien ne la vérifie.

**Règle.** Un brief d'agent en worktree **nomme le commit de base attendu**
et exige en première commande `git log --oneline -1` avec la consigne :
« sinon `git reset --hard <branche>` avant tout ». Et le rapport doit dire
sur quelle base il a travaillé.

**Corollaire.** Donner à chaque agent sa propre base de données de test
(`kalybris_test_a/b/c`) et son propre numéro de migration : deux agents
qui partagent une base se `TRUNCATE` mutuellement, et deux migrations
`012` ne se fusionnent pas.

Voir [[nommer-la-copie-visee]], [[un-rapport-d-agent-est-une-piste-pas-un-fait]].
