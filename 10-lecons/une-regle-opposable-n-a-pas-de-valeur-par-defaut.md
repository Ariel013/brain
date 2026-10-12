---
titre: Une règle opposable n'a pas de valeur par défaut
type: lecon
origine: Kalybris — 2026-10-08 (nuit)
tags: [donnees, regles, import, securite]
---

# Une règle opposable n'a pas de valeur par défaut

**Symptôme.** La revue de sécurité du catalogue relève que `ordonnance`
absent à la création et à l'import d'un produit vaut `false`. Un fichier
grossiste sans colonne « ordonnance » aurait créé 3 000 médicaments listés
en vente libre, et la validation pharmacien ne se serait jamais déclenchée
pour eux. Pas d'attaquant : c'est le cas nominal d'un import.

**Cause.** Le lecteur de saisie appliquait un défaut « confortable » à un
booléen comme aux autres — sans distinguer un champ descriptif (un
laboratoire absent ne gêne personne) d'un champ qui **porte une
obligation légale** (R01).

**Règle.** Un champ dont dépend une règle opposable — « sur ordonnance »,
« stupéfiant », « médicament », « nominatif » — est **obligatoire à
l'écriture** : absent → refus nommé (`ordonnance_manquante`), ligne par
ligne dans un import. Le défaut, s'il existe, est le **plus restrictif**,
jamais le plus permissif.

**Corollaire.** Un PUT « complet » qui remet à `null` ce que le client omet
est le même défaut sous une autre forme : omis → 400, jamais → `null`
silencieux.

Voir [[refuser-plutot-que-convertir]], [[une-enumeration-de-champs-se-teste]].
