---
titre: Pilotage financier personnel
type: projet
domaine: finances personnelles, outil mono-utilisateur
statut: amorcé le 2026-10-02, code hérité sans test
depot: ~/PROJETS/personal-finance-tracker
maj: 2026-10-02
---

# Pilotage financier personnel

**Ce que c'est.** L'outil de suivi des finances de Kevin : dépenses, revenus,
budgets, abonnements avec date d'impact budgétaire, prêts et dettes, rapport
mensuel. Repris le 2026-10-02 du projet de Yemalin Agbangla (deux commits,
avec son accord), pour l'adapter à sa vie en France. Un seul utilisateur,
jamais plusieurs (ADR 0001).

**Stack.** Next.js 16 côté client, état dans `localStorage` via un hook
central, modèle versionné avec migrations à la lecture, synchronisation
Supabase optionnelle vers un projet personnel. Vercel. Aucun test à la
reprise.

**La contrainte qui commande le reste.** Dépôt public, données réelles
sensibles : rien de réel n'entre dans le dépôt, les tests ni les captures
(ADR 0002) ; le développement se fait sur un jeu fictif.

## Ce que ce projet a appris au coffre

*(À remplir au fil des sessions.)*

## Ce qui vaudrait d'être repris ailleurs

- **Reprendre le projet d'un tiers** : historique conservé, ses commits à
  son nom, un ADR qui dit ce qu'on en fait ; l'ancien `CLAUDE.md` d'un autre
  agent devient `docs/architecture.md` au lieu d'être écrasé.
