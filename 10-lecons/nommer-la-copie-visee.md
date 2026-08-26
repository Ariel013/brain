---
titre: Dans un dépôt à plusieurs worktrees, nommer la copie visée
type: lecon
origine: Synoé — 2026-08-23
tags: [git]
---

# Dans un dépôt à plusieurs worktrees, nommer la copie visée

**Symptôme.** `git tag -a v1.5.0` lancé depuis la copie principale — restée sur
`dev` — a posé le tag sur la tête de `dev`, pas sur le commit de fusion fait dans
le worktree de release. Le tag restait **ancêtre de `main`** : un rollback aurait
atterri à côté du point de release.

**Cause.** Une commande git s'applique à la copie **courante**, pas à celle où le
travail se passe.

**Règle.** Dès qu'un second worktree existe, préfixer **toute** commande
d'écriture par `git -C <copie>` — tag, commit, merge. Et **vérifier le résultat
par ce qu'il pointe** (`git rev-parse v<tag>^{commit}` comparé à la branche), pas
par le fait que la commande n'a pas protesté.

**Corollaire.** Le worktree est justement ce qui permet de faire une release sans
arrêter le serveur de développement. Le confort a ce prix : nommer la cible.

Voir aussi [[workflow-git]], [[verifier-chaque-commit-du-decoupage]].
