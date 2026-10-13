---
titre: Optimisation CV & candidatures
type: projet
domaine: outil personnel — CV et recherche d'alternance
statut: amorcé le 2026-10-13, générateur de CV livré
depot: ~/PROJETS/optimisation_cv
maj: 2026-10-13
---

# Optimisation CV & candidatures

**Ce que c'est.** L'outil de Kevin pour décrocher une alternance de développeur
fullstack & IA : un CV généré depuis des données (JSON → HTML → PDF par
Chrome), puis une chaîne de candidature locale — collecte d'offres par API
publiques, tri par Claude Code sous l'abonnement, CV adapté par offre,
validation humaine avant tout envoi, suivi des relances.

## Ce que ce projet a appris au coffre

- Un PDF se juge à son texte extrait, pas à son rendu : Word, puis Chrome avec
  Cambria, déclarent l'accent d'un « é » décomposé comme une espace — un ATS lit
  `De veloppeur`. Candidate leçon, une seule occurrence pour l'instant.

## Ce qui vaudrait d'être repris ailleurs

- Le générateur de document « données + gabarit HTML + Chrome headless », sans
  dépendance npm, avec vérification par extraction de texte.
- L'IA sous abonnement par `claude -p` plutôt qu'une clé API, avec texte
  externe traité comme non fiable (pas de contournement des permissions).
