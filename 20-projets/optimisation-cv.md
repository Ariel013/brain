---
titre: Optimisation CV & candidatures
type: projet
domaine: outil personnel — CV et recherche d'alternance
statut: chaîne de candidature en service (CV et lettre adaptés, envoi par e-mail, candidatures spontanées), 2026-10-21
depot: ~/PROJETS/optimisation_cv
maj: 2026-10-21
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
  `De veloppeur`. Candidate leçon, une seule occurrence pour l'instant. Seconde
  trace du même terrain (2026-10-20) : un mot composé coupé en fin de ligne
  s'extrait « lui- même » et faisait refuser un PDF juste — resté au journal du
  projet.
- Session du 2026-10-20/21 (envoi d'e-mails, candidatures spontanées, RGPD) :
  [[une-action-irreversible-a-trois-issues-faite-pas-faite-incertaine]],
  [[une-reference-ajoutee-relance-le-test-de-suppression-de-la-table-visee]],
  [[une-proposition-s-affiche-elle-ne-se-preselectionne-pas]],
  [[une-frontiere-de-mot-en-francais-s-ecrit-avec-les-lettres-accentuees]],
  [[un-lien-venu-d-une-donnee-se-controle-sur-l-adresse-resolue]],
  [[un-nom-exact-n-est-pas-une-identite]],
  [[une-garde-lit-le-texte-sous-la-forme-ou-il-sera-rendu]],
  [[une-sous-requete-qualifie-la-colonne-exterieure]],
  [[arreter-un-processus-par-son-pid-pas-par-un-motif]] ; occurrences ajoutées
  à [[une-enumeration-de-champs-se-teste]],
  [[l-inscription-a-une-offre-gratuite-se-fait-avant-l-adr]],
  [[casser-le-test-expres]].
- Session du 2026-10-30/31 (Opteamis, deux CV par offre) :
  [[un-lot-qui-ecrit-sur-les-vraies-donnees-s-essaie-sur-un-seul-element]] ;
  occurrences ajoutées à [[nommer-la-copie-visee]] (CV lu dans une branche en
  retard) et [[un-vas-y-sur-un-audit-ne-vaut-pas-refonte]] (photo mise dans le
  gabarit commun au lieu de la seule candidature).

## Ce qui vaudrait d'être repris ailleurs

- L'envoi d'e-mails « brouillon exact relu, puis envoi » avec trois issues
  (fait / pas fait / incertain), réservation atomique et plafond par jour.
- La base de contacts RGPD : source et date de collecte, opposition par
  personne (adresse, LinkedIn), effacement avec liste de refus par empreinte.

- Le générateur de document « données + gabarit HTML + Chrome headless », sans
  dépendance npm, avec vérification par extraction de texte.
- L'IA sous abonnement par `claude -p` plutôt qu'une clé API, avec texte
  externe traité comme non fiable (pas de contournement des permissions).
