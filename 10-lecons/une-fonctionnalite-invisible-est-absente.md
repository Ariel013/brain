---
titre: Une fonctionnalité invisible est une fonctionnalité absente
type: lecon
origine: Synoé — 2026-08-23
tags: [front, produit]
---

# Une fonctionnalité invisible est une fonctionnalité absente

**Symptôme.** Une fonctionnalité marchait — logique testée, état vérifié, code
servi — et l'utilisatrice a signalé **deux fois** qu'elle ne marchait pas. Les
suggestions passaient par un comportement natif du navigateur : rien ne les
annonçait, et quand il n'y avait rien à suggérer, l'écran ne disait rien du tout.

**Cause.** Ce qui ne se voit pas n'existe pas pour celui qui s'en sert. Un état
vide muet se lit comme une panne.

**Règle.** Deux conséquences pratiques :
1. **Montrer** ce qu'on propose, plutôt que le cacher derrière un comportement
   implicite du navigateur.
2. **Dire qu'on attend** quand une mécanique n'a pas encore de quoi s'exprimer.

**Corollaire, pour les marches à suivre.** Une étape qui suppose un état
préalable (« le catalogue contient déjà X ») est **intestable** : elle doit
fabriquer cet état elle-même à l'étape 1. Sinon son échec sera lu comme un
défaut du logiciel.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]], [[documents-du-projet]].
