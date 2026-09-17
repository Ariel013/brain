---
titre: Un test se borne à son propre jeu de données, sans exception
type: lecon
origine: Strongman — 2026-09-17
tags: [tests, base, donnees-reelles]
---

# Un test se borne à son propre jeu de données, sans exception

**Symptôme.** Un test échouait **par intermittence** : une empreinte de
fraîcheur attendue différente restait identique.

**Cause.** Les tests tournent sur une base partagée avec les données réelles,
dans une compétition jetable créée puis supprimée. Une requête cherchait « un
passage à venir » filtrée sur le seul statut, sans l'identifiant de la
compétition de test. Elle attrapait le premier passage de **toute la base** —
celui de la compétition réelle — qu'elle faisait passer au plateau puis revenir.
L'empreinte comparée, elle, portait sur la compétition jetable, qui n'avait pas
bougé. L'échec a rendu la faute visible ; sans lui, le test aurait continué à
toucher les données réelles en silence.

**Règle.** Sur une base partagée, **toute** requête d'un test porte
l'identifiant de son jeu de données, ou un identifiant de ligne connu. Le
filtre n'est pas une optimisation : c'est la frontière entre le bac à sable et
les données réelles. Elle se vérifie par un contrôle **sur le fichier de tests
lui-même** (grep des requêtes sans filtre), pas par relecture.

Voir aussi [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]], [[une-sauvegarde-se-verifie-avant-de-detruire]].
