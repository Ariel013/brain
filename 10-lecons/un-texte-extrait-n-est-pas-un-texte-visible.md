---
titre: Un texte extrait n'est pas un texte visible
type: lecon
origine: Optimisation CV — 2026-11-05 et 2026-11-12
tags: [verification, pdf, rendu]
---

# Un texte extrait n'est pas un texte visible

**Symptôme.** Un CV d'une page passait sa vérification : une page, tous les
textes attendus présents à l'extraction, dans l'ordre. Annoncé « tient sur une
page dans toutes les variantes ». L'utilisateur l'a ouvert : le bas de la
colonne de droite était coupé au milieu d'une formation. Même défaut une
semaine plus tôt sur un autre gabarit : la dernière ligne sortait de la marge
du bas, vérification verte.

**Cause.** Le texte coupé par `overflow: hidden` (ou poussé hors de la zone
imprimable) **reste dans le PDF** : l'extraction le lit. La vérification
répondait « le texte est là », la question était « le texte se voit ».

**Règle.** Pour un rendu à hauteur fixe (page, carte, colonne), mesurer la
place **dans le moteur de rendu** : bas du dernier bloc contre bas de la zone
visible, à chaque variante. L'extraction reste utile pour l'ordre, les accents
et le compte des pages ; elle ne prouve pas qu'un texte est visible.

**Corollaire.** Un gabarit dense se resserre par paliers mesurés (le premier
qui tient), plutôt que par un réglage fixe « qui tenait la dernière fois ».

Voir [[mesurer-l-outil-avant-de-conclure]], [[une-garde-lit-le-texte-sous-la-forme-ou-il-sera-rendu]], [[regarder-l-application-fait-partie-de-la-recette]].
