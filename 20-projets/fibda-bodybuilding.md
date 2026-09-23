---
titre: FIBDA Bodybuilding
type: projet
domaine: jugement de compétition de bodybuilding en direct (FIBDA, Côte d'Ivoire)
statut: en ligne (Vercel + Turso), compétition le 2026-09-26, pas encore testé sur téléphone réel
depot: ~/PROJETS/bodybuilding_fibda
maj: 2026-09-24
---

# FIBDA Bodybuilding

**Ce que c'est.** L'application de jugement des compétitions de bodybuilding de
la fédération : inscriptions, catégories, dossards, bulletins de classement sur
le téléphone de chaque juge avec accusé serveur, calcul (retrait des extrêmes,
égalités par majorité), overall par discipline puis overall final toutes
disciplines, écran public, récompenses, sauvegarde, mode d'emploi par profil
dans l'app. Repris le 23/09/2026, trois jours avant la compétition, à partir
d'une base Python/React déjà avancée (79 tests) écrite pour ce sport.

**Stack.** Frontend React/TypeScript (Vite, PWA) conservé tel quel ; backend
**réécrit en TypeScript serverless** en une journée (Hono, libSQL/Turso,
fonctions Vercel regroupées par esbuild), au **même contrat d'API et même
modèle d'état** que le Python, avec les tests Python transposés comme oracle et
un différentiel du moteur de classement sur 200 jeux. Le Python reste un plan B
(Railway, mode proxy), en suspens.

**Les contraintes qui commandent le reste.** Le développeur n'est pas dans la
salle : tout est hébergé, documenté pour le PO (`JOURNAL.md`, `A-FAIRE.md`,
onglet « Aide »), secrets hors dépôt. Le classement ne se réécrit jamais sans
oracle : tests portés un pour un et différentiel avant de toucher au moteur.

## Ce que ce projet a appris au coffre

Session du 23 au 24 septembre 2026 (reprise, audit, réécriture, mise en ligne) :

- [[l-inscription-a-une-offre-gratuite-se-fait-avant-l-adr]] — ADR et
  procédure écrits pour une VM gratuite, le fournisseur exige un paiement
- [[une-fonction-serverless-s-envoie-regroupee-et-se-verifie-au-curl]] —
  trois « Aliased », l'API morte trois fois, la cause dans les logs seulement
- [[un-test-de-route-emprunte-le-chemin-de-l-ecran]] — 64 tests verts, la
  restauration impossible depuis l'écran

## Ce qui vaudrait d'être repris ailleurs

- **Réécrire un backend en gardant le contrat et l'état** : le frontend et les
  tests existants deviennent l'oracle au lieu d'un risque. Portage fonction par
  fonction + différentiel aléatoire Python/TS = preuve en quelques heures.
- **Mode d'emploi par profil dans l'app**, source Markdown unique, test qui
  échoue si un rôle ou un onglet n'y est pas couvert, règle dans `CLAUDE.md`
  qui l'oblige à suivre chaque changement visible.
- **Jeton de configuration** à la place de la « boucle locale » pour les
  opérations d'administration en serverless.
