---
titre: Une propriété de colonne ne survit pas à une rangée
type: lecon
origine: Synoé — 2026-08-24
tags: [front, mise-en-page]
---

# Une propriété de colonne ne survit pas à une rangée

**Symptôme.** Une bascule responsive a changé la direction d'un conteneur flex
sans reprendre ce que la direction précédente supposait : `width: 100%`,
parfaitement juste en colonne, rend chaque entrée aussi large que la barre
entière en rangée. Quatre entrées sur six sortaient de l'écran **sans que rien
ne l'indique**.

**Cause.** Le couple « conteneur qui défile + barre de défilement masquée »
transforme un défaut de largeur en **disparition silencieuse**.

**Règle.** Quand un conteneur change de direction, **relire les enfants** —
largeur, `flex`, marges — pas seulement le conteneur. Et se méfier de tout
défilement dont la barre est masquée : il cache ses propres défauts.

**Corollaire.** Ce qui doit changer avec la largeur vit **dans la feuille de
style**, pas dans un style en ligne : un style en ligne est hors d'atteinte des
requêtes média. Deux tentatives de correction ont glissé dessus avant qu'on
donne une classe au conteneur.

Voir aussi [[regarder-l-application-fait-partie-de-la-recette]].
