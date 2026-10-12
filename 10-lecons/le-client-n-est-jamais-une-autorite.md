---
titre: Le client n'est jamais une autorité — le serveur recalcule
type: lecon
origine: Kalybris — 2026-10-08 (nuit)
tags: [securite, synchronisation, hors-ligne, relecture]
---

# Le client n'est jamais une autorité — le serveur recalcule

**Symptôme.** Trois constats élevés ou moyens de la même revue, sur du code
à 100 % de tests verts : (1) une caissière crée un patient avec un plafond
d'ardoise de 50 millions et vend à crédit sans trace, alors que le plafond
est réservé au titulaire — la valeur venait de la charge utile du poste ;
(2) une clôture déclare `attendu: 0, compté: 0` et passe sans motif alors
que le serveur sait qu'il attend 18 500 ; (3) une vente datée de 1999 est
acceptée et classée sous ce jour.

**Cause.** Le contrat disait « le serveur recalcule les règles bloquantes »
et c'était fait pour le prix et la validation. Mais chaque champ **qu'on
n'avait pas listé** a été lu depuis le poste comme s'il faisait foi — le
plafond parce qu'il est « sur la fiche », l'attendu parce que le poste
l'affiche, la date parce qu'il faut bien une date.

**Règle.** Dans une charge utile venue d'un poste, chaque champ est l'un
des trois : **une donnée** (ce que l'utilisateur a saisi — gardée), **un
calcul** (recalculé par le serveur, la valeur du poste au mieux comparée et
tracée), ou **une autorité** (plafond, prix, droit — jamais lue du poste).
La relecture d'un applicateur passe chaque champ dans cette grille. Une
horloge de poste est une donnée : bornée (`[now − 45 j, now + 15 min]`),
jamais crue.

Voir [[un-refus-partage-le-predicat-de-ce-qu-il-protege]], [[la-cle-d-administration-ne-va-jamais-cote-client]].
