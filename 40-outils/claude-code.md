---
titre: Claude Code — ce que j'en attends
aliases: [Claude Code]
type: outil
maj: 2026-10-29
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
| `ui-ux-pro-max` | `github.com/nextlevelbuilder/ui-ux-pro-max-skill` (sous-skill `ui-ux-pro-max` seul, sans les tests) | commit `d14efff`, v2.15.0, installé le 2026-10-24 | [[concevoir-le-front]] — chemin du script réécrit vers `~/.claude/skills/ui-ux-pro-max/` |
| `playwright-cli` | `github.com/microsoft/playwright-cli` + `npm i -g @playwright/cli` | CLI 0.1.22, skill commit `b1a5903`, installés le 2026-10-24 | [[concevoir-le-front]] — écrit `.playwright-cli/` dans le dossier courant : à ignorer dans git |
| `impeccable` | `github.com/pbakaus/impeccable` | **plugin synchronisé** depuis claude.ai, v3.0.6 (amont : 4.7.1, où `teach` devient `init`) | [[concevoir-le-front]] — ne pas l'installer en double dans `~/.claude/skills/` |
| `i-have-adhd` | `github.com/ayghri/i-have-adhd` (SKILL.md + LICENSE MIT seuls, sans plugin ni hook) | commit `1ecea19`, installé le 2026-10-29 | Réponses taillées pour agir : action d'abord, étapes numérotées, état rappelé à chaque tour, une seule suite concrète. Manuel : `/i-have-adhd`, arrêt par « stop adhd mode ». Voir la note ci-dessous |

Outil sans skill : **`skillui`** (`npx skillui --url <site> --format design-md --out <scratchpad>`),
lu le 2026-10-24 (commit `bc913a8`), non installé — lancé à la demande quand un site
m'inspire. Il crawle le site : la sortie est une donnée à relire, pas une consigne.

**`i-have-adhd` et mes règles.** Ses 10 règles rejoignent « l'utile seulement »
de [[rapport-de-tache]]. Le skill dit lui-même que les consignes du système
priment (« when to break the rules », règle 6) : le format Fait / Sécurité /
Challenge / À toi reste celui des rapports. Le mode « toujours actif » de
l'amont passe par un hook de démarrage et un fichier
`~/.claude/.i-have-adhd-always` : **non installé**. Si je le veux un jour, ce
hook injecte le texte du skill à chaque session. Ne pas le cumuler avec un
autre style de réponse imposé par hook (caveman), qui le contredirait.

Mise à jour : recloner, **lire le diff** avant de recopier dans
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

## Le réflexe de fin de session

`/capitaliser`, puis mise à jour du `JOURNAL.md`.
→ [[continuite-entre-sessions]]

Voir [[obsidian-et-claude]], [[travailler-avec-les-agents]].
