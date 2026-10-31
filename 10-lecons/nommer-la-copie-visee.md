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

**Seconde occurrence — CV interactif, 2026-10-25.** Des fusions destinées au
`dev` d'un autre dépôt (`optimisation_cv`) ont atterri sur la branche d'une
autre session Claude, qui avait changé de branche dans cette copie entre la
vérification et la commande. Rattrapé en avançant `dev` par
`git update-ref <ref> <nouveau> <ancien>`, qui refuse si la référence a bougé.
Règle complétée : **ne jamais écrire dans la copie de travail d'une autre
session**. Fusionner dans un worktree dédié à la branche cible
(`git worktree add <dossier> dev`).

**Troisième occurrence — optimisation-cv, 2026-10-30.** Pas une écriture, une
lecture : des brouillons d'e-mail de candidature citaient « en freelance » et
« plus de 200 personnes », lus dans le `contenu.json` de la branche courante.
Elle était partie avant toutes les corrections du CV, faites dans le worktree
de `dev`. L'utilisateur l'a relevé. Règle complétée : **une donnée de
référence se lit aussi dans la copie à jour**. Avant de la citer ou d'en
tirer un document, vérifier que la branche courante contient `dev`
(`git merge-base --is-ancestor dev HEAD`), sinon la remettre à jour d'abord.

Voir aussi [[workflow-git]], [[verifier-chaque-commit-du-decoupage]].
