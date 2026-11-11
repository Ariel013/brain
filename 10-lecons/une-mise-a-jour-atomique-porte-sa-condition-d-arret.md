---
titre: Une mise à jour atomique porte sa condition d'arrêt dans son WHERE
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [concurrence, base-de-donnees, securite]
---

# Une mise à jour atomique porte sa condition d'arrêt dans son WHERE

**Symptôme.** 30 échecs de connexion simultanés posaient 3 verrous de compte (et envoyaient 3 alertes) au lieu d'un.

**Cause.** L'incrément du compteur d'échecs était atomique, mais chaque requête avait lu « pas verrouillé » avant que le premier verrou soit posé. Le compteur, remis à zéro au verrou, repartait.

**Règle.** La condition qui doit arrêter le comptage (verrou échu, essais < 5) fait partie du `WHERE` de la mise à jour atomique (`updateMany … where attempts < 5`), et l'on agit selon le nombre de lignes touchées, pas selon une lecture faite avant.

**Corollaire.** Le test qui le prouve envoie N requêtes simultanées et vérifie une borne → [[un-test-de-concurrence-verifie-la-borne-pas-le-compte]].

Voir aussi : [[un-refus-partage-le-predicat-de-ce-qu-il-protege]], [[un-echec-temporaire-ne-consomme-pas-de-tentative]]
