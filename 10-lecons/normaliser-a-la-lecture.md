---
titre: Une donnée saisie dans deux unités se normalise à la lecture
type: lecon
origine: Synoé — 2026-08-23
tags: [donnees, affichage]
---

# Une donnée saisie dans deux unités se normalise à la lecture

**Symptôme.** « 12/8 » et « 120/80 » sont la même tension, dans deux unités.
Tracées ensemble sans conversion, elles dessinent une crise qui n'a jamais eu
lieu. Et l'écran annonçait « 12/8 mmHg » — une valeur incompatible avec la vie.

**Cause.** Deux formats cohabitaient dans le même champ, et l'unité affichée
était une supposition, pas une lecture.

**Règle.** Normaliser **à la lecture**, jamais à la saisie — réécrire ce qu'un
professionnel a noté n'est pas une option. Et **ne jamais afficher une unité
qu'on n'a pas vérifiée** : mieux vaut aucune unité qu'une fausse.

**Corollaire.** Le texte libre ne supprime pas le coût de la normalisation, il
le **reporte sur la lecture**. C'est parfois le bon choix — mais c'est un choix,
il se décide et s'écrit.

Voir aussi [[refuser-plutot-que-convertir]], [[lire-le-fichier-reel-avant-de-modeliser]].
