---
titre: Une migration est additive, numérotée et journalisée
aliases: [Migrations, Discipline de migration]
type: methode
origine: Synoé, prompt d'amorce d'origine (2026-08-23), parties 3.5 et 5
maj: 2026-11-01
---

# Une migration est additive, numérotée et journalisée

**Ce qui s'est passé.** Sur Synoé, le schéma était un script `drop/recreate`
rejouable, jusqu'au jour où une utilisatrice réelle a saisi des dossiers. Une
tâche « discipline de migration » en urgence a dû passer avant tout le reste.

**La règle.** Le dossier de migrations existe **dès la première table**, avant
la première donnée réelle. Pas au moment où il y aura des données à perdre.

## La discipline

- **Additives.** Une migration ajoute ; elle ne détruit pas ce qu'une autre a
  posé.
- **Numérotées sans trou.** L'ordre d'application se lit dans le nom.
- **Idempotentes quand c'est possible** : rejouée deux fois, elle ne casse rien.
- **Un en-tête** qui dit quoi, pourquoi, quand.
- **Un renommage se fait par étapes non destructives** : ajouter le nouveau,
  recopier, basculer les lectures, retirer l'ancien dans une migration
  ultérieure.
- **Un journal d'application** tenu à jour dit ce qui est déjà passé sur
  l'environnement réel. Les migrations en attente figurent dans `A-FAIRE.md`
  → [[modele-a-faire-md]].

Un changement de schéma reste une condition d'arrêt
→ [[ce-qui-est-reversible-se-tranche-ce-qui-est-irreversible-se-demande]].
Et une référence ajoutée relance le test d'effacement de la table visée
→ [[une-reference-ajoutee-relance-le-test-de-suppression-de-la-table-visee]].

Voir aussi [[amorce-nouveau-projet]], [[poser-l-isolation-des-le-premier-schema]].
