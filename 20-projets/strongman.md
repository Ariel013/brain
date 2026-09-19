---
titre: Strongman
type: projet
domaine: arbitrage sportif en direct (FIBDA, Côte d'Ivoire)
statut: compétition tenue le 2026-09-19, résultats réparés et tracés le 20 — 205 vérifications
depot: ~/PROJETS/strongmanrepo
maj: 2026-09-20
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
- [[une-enumeration-de-champs-se-teste]] — seconde occurrence : un état
  ajouté, un message qui énumérait les états resté faux
- [[une-fonctionnalite-invisible-est-absente]] — troisième occurrence : un
  sélecteur sans option, signalé comme « ça ne prend pas »
- [[un-champ-qui-se-resynchronise-ecrase-la-frappe-en-cours]] — les noms
  tapés d'une traite perdaient leur fin, seulement en ligne

Session du 19 septembre 2026 (alertes de pesée) :

- [[une-consigne-executable-se-redige-contre-le-code]] — seconde occurrence :
  « la validation attribue le dossard », hérité du chapeau de l'original, faux
- [[verifier-chaque-commit-du-decoupage]] — troisième occurrence : statut de
  déploiement `pending` alors que la production servait déjà le commit

Sessions des 19 et 20 septembre 2026 (le jour de la compétition et le lendemain) :

- [[un-verrou-se-livre-avec-sa-voie-de-correction]] — l'ADR « plus
  d'annulation depuis le plateau » avait laissé la correction « à venir » ;
  le besoin est arrivé en pleine épreuve
- [[lire-la-donnee-avant-l-hypothese]] — « c'est les 90 secondes » : non,
  21 lignes `ok · valeur 0` en base
- [[refuser-plutot-que-convertir]] — seconde occurrence : une borne à 0
  acceptait « rien » comme une performance, à côté du verdict Zéro

Restée dans le `JOURNAL.md` du projet, parce que propre au portage : sur un
portage, la référence est l'original, pas l'intuition — un test qui échoue se
vérifie d'abord contre `docs/reference/`.

## Les patrons à reprendre ailleurs

- **L'écriture sort de l'action serveur.** Les fonctions qui décident de
  l'état vivent dans un module ordinaire, testable hors requête ; l'action
  n'ajoute que session, trace et rafraîchissement.
- **La règle de classement se relit avant de coder une demande de départage.**
  Le client a décrit sa règle avec un exemple chiffré ; elle était déjà celle
  du code. Ce qui manquait était une case de saisie, pas une règle. Vérifier
  d'abord ce que le calcul fait, répondre avec l'exemple du client, puis
  n'ajouter que ce qui manque — et consigner l'exemple dans les règles métier.
- **Un écran de pilotage règle, il n'affiche pas.** La régie a reçu deux fois
  de l'information « utile » (classement, épreuve en cours) que Kevin a fait
  retirer : ce qui se lit se lit sur les écrans pilotés, pas sur le pupitre.
- **Un barème nouveau s'écrit avec sa table** dans les règles métier, sa
  fonction pure et ses tests — le même jour (clubs : 15 / 10 / 5 / 4 / 3 / 1).
- **Ce qui se relève tout seul se relève tout seul.** Le temps au chrono se
  pose dans la case à l'arrêt du chronomètre, modifiable ; la table n'a rien
  à recopier depuis l'écran d'à côté.
- **Libérer la ressource et saisir le résultat sont deux étapes.** Quand un
  résultat dépend d'un tiers lent (le jury sur un grand terrain), l'état
  bloquant (« au plateau ») ne doit pas avoir la validation pour seule sortie.
  Un état intermédiaire « fini, résultat à saisir » garde ce que l'opérateur a
  déjà relevé, ne compte nulle part tant qu'il n'est pas rempli, et la saisie
  différée prend la forme du document qui arrive (le tableau de la feuille
  papier). ADR 0004 du projet.
- **Alerter n'est pas refuser.** À la pesée, un poids hors catégorie lève une
  alerte de couleur et laisse l'officiel décider ; le logiciel ne tranche pas
  à la place de celui qui signe. L'alerte reste après la validation : c'est
  elle qu'on cherchera en cas de réclamation.
- **Quand une valeur suit la mesure, garder celle qui dit l'annonce.** La
  catégorie affectée est recalée sur le poids pesé à la validation ; comparer
  « pesé » à « affecté » ferait donc disparaître l'alerte au moment où elle
  compte. C'est le poids déclaré, jamais réécrit, qui garde la mémoire.
- **Une réparation de données en production est un script versionné, gardé
  sur sa cible exacte.** Il compte ce qu'il s'attend à trouver (21 + 1) et
  s'arrête avant la première écriture au moindre écart ; il tourne d'abord à
  blanc et liste les lignes ; il écrit en une transaction ; il laisse au
  journal d'audit l'ancien résultat de chaque ligne ; on relit la base après.
  Relancé, il s'arrête tout seul : sa garde ne trouve plus sa cible.
- **Avant de coder une demande ambiguë qui touche une règle, poser la question
  qui la coupe en deux.** « 1 contre 1 » : passage à deux, ou duel qui change
  le classement ? La réponse a évité de toucher au barème. (Le chantier a été
  abandonné ensuite, non committé : rien à défaire.)
- **Un écart avec l'original se décide et s'écrit** (ADR), il ne s'improvise
  pas — quatre écarts nommés sur tout le portage.
- **Le papier demande exactement ce que l'écran demandera à la ressaisie, avec
  les mêmes mots**, tirés des mêmes fonctions : le juge n'a rien à traduire.
- **Empreinte de fraîcheur** : les écrans publics interrogent une signature de
  60 octets et ne redemandent la page que si elle a bougé.
