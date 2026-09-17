---
titre: Strongman
type: projet
domaine: arbitrage sportif en direct (FIBDA, Côte d'Ivoire)
statut: déployé et vérifié en ligne, avant la compétition — 168 tests
depot: ~/PROJETS/strongmanrepo
maj: 2026-09-17
---

# Strongman

**Ce que c'est.** Le logiciel d'arbitrage du Championnat National de Strongman
de la Fédération Ivoirienne de Bodybuilding, Dynamophilie et Assimilés. Il
tient la compétition **en direct, devant du public, un seul jour par an** :
athlètes, pesée, ordre de passage, chronomètre, validation des performances,
classement, mur LED. C'est le **portage** d'un poste autonome (un HTML,
`localStorage`) vers une application partagée entre postes, conservé tel quel
dans `docs/reference/` comme pièce de comparaison.

**Stack.** Next.js (App Router, Server Actions) + Drizzle + PostgreSQL sur
Supabase, déployé sur Vercel. Styles en ligne repris valeur par valeur de
l'original, pas de Tailwind. Suite fonctionnelle sur une compétition jetable.

**Les deux contraintes qui commandent le reste.** Un écran vide se lit comme
une panne : chaque cas sans donnée dit ce qu'il attend. Ce qui touche un
résultat se trace : le journal d'audit est la seule pièce en cas de
réclamation.

## Ce que ce projet a appris au coffre

Sessions des 16 et 17 septembre 2026 (déploiement, premiers retours du terrain) :

- [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]] — 5 à 8 s
  par page en production, 57 pools ouverts pour 3 requêtes
- [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]] — trois
  écritures plantaient en production sous 82 tests verts
- [[un-test-se-borne-a-son-propre-jeu-de-donnees]] — une requête sans filtre
  faisait passer au plateau un athlète de la compétition réelle
- [[verifier-chaque-commit-du-decoupage]] — seconde occurrence : un état de
  production affirmé depuis le poste local, sans l'interroger
- [[une-fonctionnalite-invisible-est-absente]] — seconde occurrence : deux
  athlètes sans passage, invisibles au plateau, lus comme un bug de filtre

Restée dans le `JOURNAL.md` du projet, parce que propre au portage : sur un
portage, la référence est l'original, pas l'intuition — un test qui échoue se
vérifie d'abord contre `docs/reference/`.

## Les patrons à reprendre ailleurs

- **L'écriture sort de l'action serveur.** Les fonctions qui décident de
  l'état vivent dans un module ordinaire, testable hors requête ; l'action
  n'ajoute que session, trace et rafraîchissement.
- **Libérer la ressource et saisir le résultat sont deux étapes.** Quand un
  résultat dépend d'un tiers lent (le jury sur un grand terrain), l'état
  bloquant (« au plateau ») ne doit pas avoir la validation pour seule sortie.
  Un état intermédiaire « fini, résultat à saisir » garde ce que l'opérateur a
  déjà relevé, ne compte nulle part tant qu'il n'est pas rempli, et la saisie
  différée prend la forme du document qui arrive (le tableau de la feuille
  papier). ADR 0004 du projet.
- **Un écart avec l'original se décide et s'écrit** (ADR), il ne s'improvise
  pas — quatre écarts nommés sur tout le portage.
- **Le papier demande exactement ce que l'écran demandera à la ressaisie, avec
  les mêmes mots**, tirés des mêmes fonctions : le juge n'a rien à traduire.
- **Empreinte de fraîcheur** : les écrans publics interrogent une signature de
  60 octets et ne redemandent la page que si elle a bougé.
