---
titre: Synoé
type: projet
domaine: santé au travail
statut: en production (pilote mono-cabinet)
depot: ~/PROJETS/synoe
maj: 2026-09-08
---

# Synoé

**Ce que c'est.** Un logiciel de gestion de médecine du travail (PWA
React/TypeScript) qui remplace les fichiers Excel d'une médecin du travail :
dossiers salariés, aptitudes, agenda, pharmacie d'infirmerie, import de données
existantes, espace patient. Conçu **multi-cabinet dès le schéma**, en phase
pilote avec **une seule utilisatrice réelle**.

**Stack.** React 18 + TypeScript + Vite, PWA offline-first · Zustand ·
IndexedDB en local et Postgres/Supabase en option derrière un contrat `Repo` ·
RLS par `cabinet_id` · déploiement Cloudflare.

## Ce que ce projet a appris au coffre

C'est de loin la plus grosse contribution du coffre à ce jour — presque toutes
les notes de [[lecons]] en viennent. Les plus structurantes :

- [[verifier-le-chemin-d-ecriture]] — deux jours en production sans persistance
- [[un-selecteur-lit-il-ne-calcule-pas]] — trois écrans tués par un `?? []`
- [[le-calcul-sort-de-l-ecran]] — quatre défauts d'import, une seule cause
- [[stager-nommement]] — des données sensibles committées par une commande large
- [[ecrire-la-decision-avec-le-code]] — 5 000 lignes livrées sans ADR ni tests
- [[regarder-l-application-fait-partie-de-la-recette]] — 480 tests verts, trois écrans blancs
- [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]] — « typecheck vert » sur un lot qui ne compilait pas
- [[une-consigne-executable-se-redige-contre-le-code]] — une marche à suivre écrite depuis le journal

## Les patrons à reprendre ailleurs

- [[isoler-la-persistance-derriere-un-contrat]] — le contrat `Repo` (ADR 0002)
- [[poser-l-isolation-des-le-premier-schema]] — `cabinet_id` dès le jour 1 (ADR 0001)
- **La structure documentaire complète** — c'est elle qui a servi de base à
  [[documents-du-projet]] et aux [[modeles]].
- **L'écriture additive** plutôt que la modification en place, sur un domaine où
  l'historique fait foi.
- **Le journal d'audit en couche applicative** plutôt qu'en triggers : lisible,
  testable, et l'action reste du texte libre côté base pour ne pas exiger une
  migration à chaque nouveau verbe.

## Contraintes propres au domaine

Elles ne se généralisent pas, mais elles rappellent qu'un domaine impose ses
règles avant l'architecture :

- **Le secret médical prime** : un rôle non-médical n'accède jamais au contenu
  médical, quelle que soit la légitimité de son accès au système.
- **Pas d'API IA externe** avec des données de patient tant que ce n'est pas
  explicitement rouvert, et jamais en appel direct depuis le client.
- **Portabilité et effacement** doivent exister avant d'ouvrir à d'autres
  utilisateurs réels.
- **Pas de bibliothèque de graphiques** : CSS/SVG inline, pour rester léger et
  fonctionner hors ligne.

## Où regarder dans le dépôt

`CLAUDE.md` (règles), `JOURNAL.md` (état + leçons complètes), `docs/decisions/`
(18 ADR), `docs/architecture.md` (le pourquoi), `A-FAIRE.md` (prérequis
externes).
