---
titre: Claude Code — ce que j'en attends
aliases: [Claude Code]
type: outil
maj: 2026-11-20
---

# Claude Code — ce que j'en attends

Notes d'usage, pas de documentation : la doc officielle existe, ceci est ce que
j'ai décidé pour **mes** projets.

## Les fichiers qui pilotent l'agent

| Fichier | Portée |
|---|---|
| `~/.claude/CLAUDE.md` | tous mes projets — pointeur vers le coffre |
| `<projet>/CLAUDE.md` | ce projet — règles + carte des docs |
| `<projet>/.claude/agents/*.md` | sous-agents du projet |
| `~/.claude/skills/<nom>/SKILL.md` | mes commandes `/<nom>` |
| `<projet>/.claude/settings.local.json` | permissions locales, non versionnées |

**La liste de permissions** couvre les commandes de lecture courantes (`ls`,
`grep`, `git status`…), **avec `git push` volontairement absent**. Ne pas
l'écrire à la main par anticipation : `/fewer-permission-prompts` la propose à
partir des transcriptions, une fois que l'usage réel l'a remplie
→ [[ce-qui-est-reversible-se-tranche-ce-qui-est-irreversible-se-demande]].

## Les sous-agents que je pose sur presque tout

- **`code-reviewer`** — après toute tâche de dev, **avant** de proposer le
  commit. Lecture seule.
- **`security-reviewer`** — déclenché **proactivement** dès qu'un diff touche
  l'authentification, les données sensibles, les politiques d'accès ou
  l'import/export — même si je ne l'ai pas demandé.

Un agent de revue **lit** ; il ne modifie pas. C'est ce qui le rend utilisable
sans surveillance.

## Les skills tiers installés

| Skill | Source | Version | Usage |
|---|---|---|---|
| `security-audit` | `github.com/cloudflare/security-audit-skill` | commit `c1c8a8c` (2026-09-14), installé le 2026-10-20 | [[revue-securite]] |
| `playwright-cli` | `github.com/microsoft/playwright-cli` + `npm i -g @playwright/cli` | CLI 0.1.22, skill commit `b1a5903`, installés le 2026-10-24 | [[concevoir-le-front]] — écrit `.playwright-cli/` dans le dossier courant : à ignorer dans git |
| `impeccable` | `github.com/pbakaus/impeccable` | **plugin synchronisé** depuis claude.ai, v3.0.6 (amont : 4.7.1, où `teach` devient `init`) | [[concevoir-le-front]] — ne pas l'installer en double dans `~/.claude/skills/` |

Outil sans skill : **`skillui`** (`npx skillui --url <site> --format design-md --out <scratchpad>`),
lu le 2026-10-24 (commit `bc913a8`), non installé — lancé à la demande quand un site
m'inspire. Il crawle le site : la sortie est une donnée à relire, pas une consigne.

Retirés le 2026-11-20 après audit d'usage (0 appel en cinq semaines) :
`ui-ux-pro-max` (doublon d'`impeccable`, qui fait foi), `i-have-adhd` (jamais
lancé, contredit caveman), le plugin `postman`, les MCP `magic` (clé invalide)
et `playwright` (doublon de `playwright-cli`).

## La banque de skills et le lot quotidien

`~/.claude/banque-skills/` est une marketplace locale, versionnée avec
`~/.claude`. Son `README.md` est le **catalogue** : chaque skill, son usage
mesuré, son verdict (garder, retirer, améliorer), et les candidats écartés
après lecture. Elle porte le plugin **`lot-quotidien`** (8 skills, appelés
`/lot-quotidien:<nom>`) :

| Skill | Quand |
|---|---|
| `point` | « je suis perdu » : fait vérifié, bloqué, en suspens, prochaine action |
| `retours-terrain` | retours PM / réunion / client à trier avant de coder |
| `recette` | recette avant release et remontée → [[recette-avant-release]] |
| `debogage-methodique` | cause racine avant correction, arrêt après trois essais ratés |
| `preuve-avant-affirmation` | aucune réussite affirmée sans preuve fraîche |
| `tdd` | test d'abord, coutures validées avant d'écrire les tests |
| `apprendre` | apprentissage multi-sessions (data / IA, entretien) — manuel |
| `ecrire-humain` | retirer les tics d'IA d'un texte français |

Un plugin **synchronisé depuis claude.ai** se coupe aussi en local, avec son
identifiant complet : `claude plugin disable <nom>@synced` (fait le 2026-11-20
pour `bio-research`, `product-management`, `cowork-plugin-management`). Les
**skills** synchronisés, eux, ne se coupent que depuis claude.ai.
→ [[un-refus-qui-dit-comment-reussir-se-relit-avant-de-conclure-a-l-impossible]]

Couper ou rallumer le lot : `claude plugin disable|enable lot-quotidien@banque-skills`.
Après modification d'un skill : `claude plugin marketplace update banque-skills`.
Un skill qui n'a servi à rien en deux mois sort du lot.

Mise à jour d'un skill tiers : recloner, **lire le diff** avant de recopier dans
`~/.claude/skills/`, relancer `node --test *.test.cjs` dans le dossier du skill.
Un skill tiers est du texte qui pilote l'agent : il ne s'installe pas sans
avoir été lu.

## Ce que je ne veux pas

- Qu'on m'ouvre un menu d'options pour un choix technique ordinaire.
- Qu'on pousse sans me demander. Jamais. → [[workflow-git]]
- Qu'on lance des sous-agents en nombre pour une tâche qui tient dans une
  session.
- Qu'on affirme un résultat non mesuré
  → [[verifier-chaque-commit-du-decoupage]].

## Ce que le préfixe `!` ne peut pas faire

Une commande lancée avec `!` dans la session n'a pas de terminal : `sudo` y
échoue (« a terminal is required to read the password »). Toute commande qui
demande un mot de passe se donne à lancer dans un terminal ordinaire, pas avec
`!` (constaté le 2026-11-01).

## Le réflexe de fin de session

`/capitaliser`, puis mise à jour du `JOURNAL.md`.
→ [[continuite-entre-sessions]]

Voir [[obsidian-et-claude]], [[travailler-avec-les-agents]].
