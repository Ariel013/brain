---
titre: Un .env ne se source pas dans le shell — il se donne au programme
type: lecon
origine: Optimisation CV — 2026-11-12
tags: [securite, secrets, shell]
---

# Un .env ne se source pas dans le shell — il se donne au programme

**Symptôme.** Pour un essai, un agent a chargé le `.env` du projet par
`set -a; . ./.env; set +a`. La sortie a affiché
`./.env:15: command not found: <quatre caractères>` : un morceau d'un mot de
passe d'application, écrit dans le journal de la session.

**Cause.** Le format `.env` n'est pas du shell. Une valeur non citée qui
contient des espaces (un mot de passe d'application Google s'écrit par blocs
de quatre) est découpée : le shell exécute le reste comme une commande, et son
message d'erreur recopie la valeur.

**Règle.** Ne jamais sourcer un `.env` dans le shell. Le donner au programme
qui le lit (`node --env-file`, `tsx --env-file-if-exists=.env`, le chargeur du
framework), qui ne l'exécute pas. Un essai ponctuel passe par le même lanceur
que les scripts du projet.

**Corollaire.** Un fragment de secret apparu dans une sortie se signale ; la
rotation se décide avec l'utilisateur selon l'endroit où la sortie est allée.

Voir [[un-rapport-qui-signale-une-donnee-sensible-ne-la-recopie-pas]], [[la-cle-d-administration-ne-va-jamais-cote-client]].
