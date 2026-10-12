---
titre: Kalybris
type: projet
domaine: pharmacie d'officine (Côte d'Ivoire)
statut: sprints 0 et A terminés — socle poste et serveur, 168 tests
depot: ~/PROJETS/Kalybris
maj: 2026-09-06
---

# Kalybris

**Ce que c'est.** Un logiciel de gestion d'officine (LGO) pour la Côte
d'Ivoire, qui reprend et dépasse l'existant (Médiciel). Deux différenciants
revendiqués : la traçabilité de lot **FEFO + DataMatrix**, que Médiciel n'a
pas du tout, et le **suivi à distance de l'officine, y compris hors du
territoire ivoirien** — objectif de base du projet, pas une option.

**Stack.** React 18 + Vite + TypeScript strict + Dexie (IndexedDB) + Workbox
(PWA offline-first) · Node 20 + Fastify + PostgreSQL 16 avec RLS par
`officine_id` · JWT **RS256**, clé privée cloud uniquement · agent local Rust
pour les périphériques (imprimante, douchette, tiroir-caisse).

**La contrainte qui commande tout le reste :** aucun flux de données hors
CEDEAO sans autorisation ARTCI. Elle exclut par défaut Sentry, Datadog, et la
quasi-totalité des outils SaaS de sécurité du marché. Ce n'est pas une
préférence, c'est la loi 2013-450.

## Ce que ce projet a appris au coffre

Session du 05/09/2026 (Sprint 0, audit d'un prototype livré par un tiers) :

- [[un-garde-fou-trop-large-empeche-sa-propre-documentation]] — le hook qui
  bloque les push a refusé le fichier qui le documentait, puis son propre
  correctif
- [[une-fonctionnalite-mise-en-scene-est-pire-qu-absente]] — une maquette qui
  affiche « reprise auto au retour du réseau » sans reprise fait croire au
  décideur que le sujet est traité
- [[un-rapport-d-agent-est-une-piste-pas-un-fait]] — deux affirmations
  d'agents corrigées après vérification directe à la source
- [[un-budget-de-poids-est-une-contrainte-de-perimetre]] — mesurer le socle
  vide transforme un principe (« restons légers ») en arbitrage chiffré
- [[un-rapport-qui-signale-une-donnee-sensible-ne-la-recopie-pas]] — l'audit
  qui dénonçait la fuite l'a d'abord recopiée, puis committée
- [[un-tri-sur-une-colonne-castee-trie-sur-le-cast]] — une chaîne d'audit
  vérifiée dans l'ordre 10, 11, 9 ; le défaut n'apparaît qu'à la dixième ligne
- [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]] — purger un
  journal append-only sans y percer de porte

Session du 07/10/2026 (recette et revue de sécurité du Sprint A) :

- [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]] —
  sous le rôle de production, la purge ne voyait rien, concluait que rien ne
  manquait, et supprimait ; les tests tournaient en superutilisateur
- [[un-mecanisme-de-detection-se-teste-en-continuant-apres-la-detection]] —
  les points de contrôle du journal se laissaient recouvrir au redémarrage
  suivant ; le test s'arrêtait au moment où l'alerte sonne
- Deux règles plus courtes, gardées dans `DECISIONS_LOG.md` du projet, à
  promouvoir si elles reviennent ailleurs : *un compteur de sécurité
  s'incrémente dans la base, en une instruction, et c'est la valeur rendue
  qui décide* ; *chaque branche de refus d'une connexion coûte le même temps
  et rend le même corps*.

## Les patrons à reprendre ailleurs

- **Rendre lisible avant d'auditer.** Le livrable était un HTML
  auto-extractible de 2,4 Mo : illisible, indiffable, invisible en revue, et
  opaque à tout scanner de secrets. Écrire le script d'extraction *avant*
  l'audit a été le meilleur investissement de la session — et l'extraction
  s'est vérifiée par comparaison SHA-256, pas par confiance.
- **Le garde-fou s'écrit avec sa recette, du premier jet.** 31 cas, dont
  autant de faux positifs à ne pas produire que de contournements à bloquer.
  Voir [[stager-nommement]], même famille de problème.
- **Auditer à plusieurs voix en parallèle**, chacune avec son référentiel
  propre (technique, produit/légal, design, sécurité) — puis revérifier soi-même
  les constats qui vont fonder une décision.
- **Séparer « interdit par un document du projet » de « me semble risqué ».**
  Confondre les deux fait perdre la confiance dans les deux.

## Contraintes propres au domaine

Elles ne se généralisent pas, mais elles rappellent qu'un domaine impose ses
règles avant l'architecture. Le cahier des charges porte **14 règles
opposables R01-R14**, chacune avec son fondement légal *et* son test attendu —
c'est le référentiel le plus opérationnel du corpus, et c'est celui que le PRD
avait oublié de citer :

- **R01** — aucune vente de médicament sans qu'un pharmacien inscrit soit
  identifié comme responsable. Test : rejet 403.
- **R05** — le prix d'un médicament homologué est en **lecture seule** au
  comptoir. Aucune remise, aucune exception.
- **R06** — aucun point de fidélité sur un médicament. Test : panier de
  médicaments, cumul **nul**.
- **R08** — aucune mesure clinique, aucun dépistage, aucun avis médical au
  comptoir. Même offert.
- **R12** — aucune donnée personnelle hors CEDEAO ; aucune destination hors
  zone **activée par défaut**.
- **R13** — aucune décision affectant une personne sur le seul fondement d'un
  traitement automatisé.

Sont explicitement retirés du produit, par la loi ou la déontologie : vente en
ligne de médicaments, ordonnance par messagerie, substitution automatique,
pointeuse biométrique.

## Où regarder dans le dépôt

`CLAUDE.md` (point d'entrée) · `docs/brain/STATE.md` (**à lire en premier**) ·
`docs/brain/DECISIONS_LOG.md` · `docs/AUDIT-PROTOTYPE.md` (ce qu'est vraiment
le front livré) · `docs/TASKS.md` (backlog + 19 décisions humaines en attente) ·
`docs/OUTILLAGE-AGENTS.md`.

## Session autonome du 08/10 (nuit) → 09/10

Le chef de projet a laissé la session avancer seule. Résultat : Sprint B
clos, Sprint C complet (serveur + poste), Sprint D serveur, trois revues de
sécurité (8 élevés corrigés), une recette QA sur serveur réel, 83 commits
non poussés, 703 tests, 115 Kio de bundle. Détail : `docs/brain/SESSION_LOG.md`.

**Ce qui a marché :** écrire le contrat (`docs/CONTRAT-SPRINT-C.md`) avant
de lancer front et serveur en parallèle ; un worktree, une base de test et
un numéro de migration par agent ; relecture adverse après chaque tranche,
avec reproduction obligatoire.

**Ce qui a coûté :** les worktrees partent de `main` (quatre reprises) ;
deux agents tombés sur des timeouts d'API, repris sans perte par message ;
les conflits de fusion dans `serveur.ts` et `ventes.ts`, résolus à la main.

Leçons montées : [[un-worktree-d-agent-part-de-main-pas-de-la-branche-courante]],
[[une-regle-opposable-n-a-pas-de-valeur-par-defaut]],
[[un-acte-passe-se-juge-sur-des-faits-dates-jamais-sur-un-etat-courant]],
[[le-client-n-est-jamais-une-autorite]],
[[un-echec-temporaire-ne-consomme-pas-de-tentative]],
[[une-cle-un-usage-un-texte-signe-dit-a-quoi-il-sert]],
[[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]].
