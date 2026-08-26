---
titre: Le calcul ne vit pas dans un composant
type: lecon
origine: Synoé — 2026-08-22
tags: [architecture, tests, front]
---

# Le calcul ne vit pas dans un composant

**Symptôme.** Quatre défauts coûteux d'un import — cinq lignes lues au lieu de
trente, le jeu de démonstration chargé à la place du vrai fichier, des colonnes
jetées, une date perdue — partageaient **une seule cause**.

**Cause.** Ils vivaient dans le composant d'écran, hors de portée de tout test.
Chaque fonction, prise seule, était correcte ; c'est **le trajet complet** qui
était faux, et rien ne l'exerçait.

**Règle.** Dès qu'un écran calcule, **le calcul sort dans une lib**, et un test
le déroule de bout en bout **sur une entrée réelle**. Un composant ne contient
que du rendu et de l'état d'affichage.

**Corollaire.** Quand un défaut est trouvé dans un écran, **extraire avant de
corriger** — sinon le défaut suivant s'y installera au même endroit.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]], [[lire-le-fichier-reel-avant-de-modeliser]].
