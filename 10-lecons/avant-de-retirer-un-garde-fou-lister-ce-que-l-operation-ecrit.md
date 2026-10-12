---
titre: Avant de retirer un garde-fou, lister tout ce que l'opération écrit
type: lecon
origine: Kalybris — 2026-10-10
tags: [securite, decision, relecture]
---

# Avant de retirer un garde-fou, lister tout ce que l'opération écrit

**Symptôme.** Une borne anti-antidatage bloquait la reprise légitime d'une
clôture. Je l'ai restreinte aux ventes en raisonnant : « elle existe pour
empêcher qu'on forge une validation d'ordonnance ; seule la vente en porte
une ». La revue suivante a reproduit qu'une annulation antidatée écrivait
une rectification **datée avant la sortie qu'elle rectifie** au registre
légal des stupéfiants, et qu'un règlement antidaté sortait une dette des
relances.

**Cause.** J'ai justifié le garde-fou par **le vecteur qui l'avait fait
naître**, pas par **tout ce qu'il protégeait** à la date où je le retirais.
Entre-temps, l'annulation s'était mise à écrire au registre.

**Règle.** Avant d'assouplir un garde-fou sur une opération, lister ce que
l'opération **écrit aujourd'hui** (tables, registres, journaux, effets sur
d'autres calculs) et vérifier pour chaque écriture que l'assouplissement ne
la rend pas falsifiable. Si le motif de l'assouplissement ne concerne qu'un
cas (ici : la reprise d'une clôture), restreindre **à ce cas**, pas à son
complémentaire.

Voir [[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]], [[un-acte-passe-se-juge-sur-des-faits-dates-jamais-sur-un-etat-courant]].
