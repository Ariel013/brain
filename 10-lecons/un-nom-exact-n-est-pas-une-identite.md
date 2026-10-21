---
titre: Un nom exact dans un annuaire n'est pas une identité
type: lecon
origine: Optimisation CV — 2026-10-21
tags: [donnees, rapprochement, annuaire]
---

# Un nom exact dans un annuaire n'est pas une identité

**Symptôme.** Pour compléter des entreprises (SIREN, taille), la règle « un
seul candidat de l'annuaire porte exactement ce nom → on le retient » a été
mesurée sur 55 entreprises réelles : « EDF » tombait sur une petite société
homonyme, « Siemens » sur une PME sans effectif, « Qare » sur une entité d'une
autre ville. Et l'effectif d'une entité juridique trompait pour un groupe
(Alstom : « 1 ou 2 salariés » au siège).

**Cause.** Un annuaire officiel contient des coquilles homonymes, des sièges,
des filiales ; le nom commercial est souvent un sigle de la raison sociale.
L'unicité du nom exact dans **les résultats retournés** ne dit rien de
l'entité qu'on cherche.

**Règle.** Une correspondance automatique exige **une preuve de plus que le
nom** (sigle, taille connue, catégorie ; la plus grosse seulement si elle est
seule à son rang), sinon elle se montre et l'humain choisit. Et la règle se
mesure sur les vraies données avant d'être dite sûre.

Voir [[lire-la-donnee-avant-l-hypothese]], [[une-frontiere-de-mot-en-francais-s-ecrit-avec-les-lettres-accentuees]].
