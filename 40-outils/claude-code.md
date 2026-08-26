---
titre: Claude Code — ce que j'en attends
aliases: [Claude Code]
type: outil
maj: 2026-08-26
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
