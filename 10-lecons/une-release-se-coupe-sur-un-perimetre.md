---
titre: Une release se coupe sur un périmètre décidé
type: lecon
origine: Synoé — 2026-08-23
tags: [git, release]
---

# Une release se coupe sur un périmètre décidé

**Symptôme.** Une version a été taguée, puis le travail a continué sur `dev`. La
release préparée ne contenait déjà plus tout. Il a fallu choisir entre reporter
le nouveau travail et rejouer toute la promotion.

**Cause.** La release avait été coupée sur **l'état de `dev`** — une cible
mouvante — au lieu d'un périmètre énoncé.

**Règle.** Avant de taguer : **dire ce que la release contient, et s'arrêter
là**. Si le travail doit continuer, préparer la release **après**, pas avant.

**Corollaire.** « Rien n'est poussé » est ce qui rend une erreur de release
réparable : tant que rien n'est parti, rejouer coûte peu. Une fois poussé, ce
serait un force-push sur `main` — c'est-à-dire non. Une raison de plus de ne
jamais pousser sans y avoir réfléchi.

Voir aussi [[workflow-git]], [[recette-avant-release]].
