---
titre: Un test qui porte la formule la protège, il ne la vérifie pas
type: lecon
origine: Kalybris — 2026-10-10
tags: [tests, metier, relecture]
---

# Un test qui porte la formule la protège, il ne la vérifie pas

**Symptôme.** L'attendu de caisse soustrayait deux fois la monnaie rendue :
pour une vente de 4 000 payée 5 000, le tiroir gagne 4 000, le serveur en
attendait 3 000 — chaque clôture honnête aurait demandé un motif d'écart.
Le test vert s'intitulait « = espèces des ventes − monnaie rendue +
règlements » et attendait 3 000. La recette du matin avait noté « vente
1 600, monnaie 400, attendu 1 200 » sans le relever. Trouvé le soir, par
hasard, en relisant un autre correctif qui reprenait la même formule.

**Cause.** Le test avait été écrit **depuis le code** (on recopie la formule,
on calcule ce qu'elle donne) et non **depuis le monde** (qu'y a-t-il dans
le tiroir ?). Un test qui recopie l'implémentation garantit seulement
qu'elle ne change pas.

**Règle.** Un test de calcul métier part d'un **fait observable** — le
contenu du tiroir, le solde du compte, le stock sur l'étagère — écrit en
commentaire avec ses chiffres, puis attend ce fait. Son titre décrit le
monde, jamais la formule. Une recette qui lit un nombre le recalcule à la
main avant de cocher.

Voir [[une-consigne-executable-se-redige-contre-le-code]], [[casser-le-test-expres]].
