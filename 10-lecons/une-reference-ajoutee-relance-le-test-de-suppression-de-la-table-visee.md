---
titre: Une référence ajoutée vers une table relance le test de suppression de cette table
type: lecon
origine: Optimisation CV — 2026-10-21
tags: [donnees, rgpd, migration, tests]
---

# Une référence ajoutée vers une table relance le test de suppression de cette table

**Symptôme.** L'effacement d'un contact à sa demande (RGPD) marchait et était
testé. Le lendemain, une migration a ajouté `envois.contact_id REFERENCES
contacts(id)` pour les candidatures spontanées. Effacer une personne déjà
écrite levait désormais une erreur de contrainte : le droit promis ne tenait
plus, et aucun test ne l'a vu — le test d'effacement portait sur un contact
jamais écrit.

**Cause.** Une clé étrangère change le contrat de **la table visée**, pas
seulement celui de la table qui la porte. libSQL applique les clés étrangères
par défaut (`pragma foreign_keys` = 1, mesuré). Et même sans contrainte, la
ligne liée gardait l'adresse et le message de la personne effacée.

**Règle.** Quand une table gagne une référence vers une autre, écrire (ou
relancer) le test de **suppression** de la table visée **avec une ligne liée**.
Décider explicitement ce que devient la ligne liée : anonymisée, détachée
(`SET NULL`), ou suppression refusée — jamais par défaut.

Voir [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]], [[une-enumeration-de-champs-se-teste]].
