---
titre: FIBDA CONNECT
type: projet
domaine: plateforme fédérale (FIBDA, Côte d'Ivoire) — registre, inscriptions en ligne, paiements, puis conduite des compétitions
statut: prototype d'inscription en ligne sur Vercel, présentation à la fédération le 2026-11-13
depot: ~/PROJETS/Fibda-connect
maj: 2026-11-11
---

# FIBDA CONNECT

**Ce que c'est.** La plateforme commune de la fédération, prévue pour plusieurs années. Le cahier des charges v1.0 (8 nov 2026, 46 pages) couvre registre, inscriptions, paiements, badges, conduite des quatre disciplines et réseau local. La v1 se limite au socle et aux inscriptions. Elle succède aux applications séparées [[fibda-bodybuilding]] et [[strongman]], qu'elle intégrera par adaptateur sans les réécrire.

**Stack.** Monorepo pnpm, Next.js 16 + next-intl, NestJS à venir, Zod partagé dans `packages/shared`, PostgreSQL + Prisma. Le prototype tourne sans API ni base : brouillon en mémoire, tout est signalé DÉMO.

**Les contraintes qui commandent le reste.** Le serveur est seul maître du numéro FIBDA et de toute autorisation. Isolation par édition, garantie par clés étrangères composites. Tout est documenté, mode d'emploi compris (ADR-028). Le cahier et les maquettes restent hors de Git, car une maquette contenait des fiches nominatives.

## Ce que ce projet a appris au coffre

Session du 2026-11-10 (lecture du kit, audit des maquettes, modèle, prototype, carte du parcours, mise en ligne) :

- [[un-bouton-qui-apparait-sous-le-doigt-recoit-le-second-appui]]
- [[un-champ-conditionnel-masque-se-purge-il-ne-se-cache-pas]]
- [[un-select-qui-agit-au-changement-agit-a-chaque-fleche]]
- seconde occurrence de [[un-refus-partage-le-predicat-de-ce-qu-il-protege]] (effacement d'erreurs par chemin exact)
- seconde occurrence de [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]] (contrôle enchaîné au commit sans le bloquer)
- deux prérequis ajoutés à [[amorce-nouveau-projet]] : vérifier que la maquette contient l'écran prioritaire ; lire les fichiers reçus d'un tiers avant tout `git add`

Sessions du 2026-11-10 au 2026-11-11 (API, auth, Turnstile, nuits autonomes, intégration de l'ensemble) :

- [[un-test-de-concurrence-verifie-la-borne-pas-le-compte]]
- [[un-peripherique-simule-par-les-tests-ne-voit-pas-l-en-tete-qui-l-interdit]]
- [[un-en-tete-ajoute-par-les-tests-part-aussi-vers-les-tiers]]
- [[une-csp-du-premier-chargement-vaut-pour-toute-la-navigation-cote-client]]
- [[une-mise-a-jour-atomique-porte-sa-condition-d-arret]]

## Ce qui vaudrait d'être repris ailleurs

- **Carte de décision interactive** pour un commanditaire : phases → points à trancher → options avec avantages, inconvénients et conséquences sur les autres phases. Chaque point est étiqueté « fixé par le cahier », « à décider » ou « proposition ». Synthèse imprimable, choix gardés dans l'appareil.
- **Prototype sans persistance mais pas jetable** : schémas et règles partagés, stockage derrière un contrat, en mémoire d'abord.
- **Revue des coutures après intégration** : chaque branche revue seule, puis une revue de sécurité dédiée aux points de contact entre branches (idempotence × routes publiques, proxy × IP cliente, CSP × script tiers). Elle a trouvé deux constats importants que les revues par branche n'avaient pas vus.
- **Revue en deux agents indépendants** (design, QA adverse) sur un serveur figé : 20 constats que les tests verts n'avaient pas vus.
