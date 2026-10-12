---
titre: Des tests verts ne remplacent pas une relecture adverse
type: lecon
origine: Kalybris — 2026-10-09 (petit matin)
tags: [securite, revue, tests, agents]
---

# Des tests verts ne remplacent pas une relecture adverse

**Symptôme.** Une nuit, trois tranches livrées par des agents, chacune avec
ses tests (de 222 à 375 tests serveur, tous verts, dont un par règle
opposable). Trois revues de sécurité, chacune lancée sur du code
« terminé » : **8 constats élevés**, tous reproduits par un script — ancre
forgeable par le rôle applicatif, plafond posé par la caissière, session
révoquée acceptée, file qui abandonne une vente, jeton stocké sans usage,
déclassement d'un stupéfiant, validation jugée sur l'état présent, une
seule clé pour tout. Aucun n'avait de test qui le cherchait.

**Cause.** Un test vérifie ce que l'auteur a pensé ; l'auteur d'une tranche
pense depuis la règle (« R05 : prix égal au catalogue ») et écrit le test
de la règle. Le contournement vit **à côté** de la règle, dans un champ
que personne n'a listé — et le même agent ne le verra pas en relisant.

**Règle.** Toute tranche qui touche auth, argent, santé ou registre passe
par une **relecture adverse par un autre agent**, avec consigne de
**reproduire** chaque constat avant de l'écrire (un constat faux coûte plus
qu'un constat manqué — déjà payé le 07/10). Chaque constat se corrige avec
un test joué avant (échec) et après (succès), et sa règle monte en ADR.
Coût mesuré : une revue coûte moins qu'une des tranches qu'elle relit.

Voir [[un-rapport-d-agent-est-une-piste-pas-un-fait]], [[casser-le-test-expres]], [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]].
