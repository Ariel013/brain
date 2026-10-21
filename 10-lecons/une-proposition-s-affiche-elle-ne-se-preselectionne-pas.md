---
titre: Une proposition s'affiche, elle ne se présélectionne pas quand le choix engage
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [ui, formulaire, consentement]
---

# Une proposition s'affiche, elle ne se présélectionne pas quand le choix engage

**Symptôme.** Pour chaque compétence proposée, la catégorie du CV suggérée par
un dictionnaire était présélectionnée dans la liste. Or « cochée sans
catégorie » voulait dire « plan d'apprentissage seulement ». Avec la
présélection, cet état n'existait plus : une compétence cochée pour être
apprise entrait dans le CV au premier clic sur « Ajouter » — un fait non
voulu sur un document envoyé à des recruteurs. Relevé en relecture.

**Cause.** Présélectionner une valeur, c'est prendre la décision à la place de
l'utilisateur et lui demander de la défaire. Ça passe pour un confort tant
que la valeur ne fait que suggérer ; ça devient une écriture silencieuse dès
que le formulaire sert à **plusieurs** intentions.

**Règle.** Quand un choix fait entrer une donnée qui engage (un fait dans un
document, un envoi, un paiement), la proposition s'**affiche** (« proposée »)
et la valeur par défaut est le choix **neutre** (« ne pas l'ajouter »).

Voir [[une-regle-opposable-n-a-pas-de-valeur-par-defaut]], [[ce-que-l-ecran-promet-le-code-le-fait]].
