---
titre: Lire le fichier réel avant de modéliser
type: lecon
origine: Synoé — 2026-08-22
tags: [donnees, import, produit]
---

# Lire le fichier réel avant de modéliser

**Symptôme.** Le fichier de l'utilisatrice **ressemblait** à une liste de
personnes. C'était en réalité un registre d'événements où chaque ligne est une
copie de la précédente, augmentée. Le modèle « une ligne = une fiche » qu'on en
avait déduit créait **un doublon par événement**.

**Cause.** La structure avait été lue dans les **en-têtes de colonnes**, pas dans
les données.

**Règle.** Avant de décider d'une forme de données à partir d'un export :
**regrouper les lignes et chercher ce qui se répète**. La structure est dans les
répétitions, pas dans les en-têtes.

**Plus généralement.** Un export produit par un humain porte sa manière de
travailler. Le modéliser sans l'avoir regardé, c'est modéliser sa propre
supposition.

Voir aussi [[le-calcul-sort-de-l-ecran]], [[normaliser-a-la-lecture]].
