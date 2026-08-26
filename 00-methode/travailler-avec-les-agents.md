---
titre: Travailler avec les agents
aliases: [Agents, Claude, Méthode agent]
type: methode
maj: 2026-08-26
---

# Travailler avec les agents

Ce que j'attends d'un agent sur mes projets, et ce que j'ai appris de ce qui se
passe mal.

## Ce que je veux

- **Qu'il tranche.** Les choix techniques ordinaires se décident au mieux du
  projet, sans me soumettre une liste d'options. Une recommandation, pas un menu.
- **Qu'il s'arrête sur l'ambigu structurant.** Nouvelle table, nouveau flux,
  changement de convention : on expose, on décide, on écrit l'ADR, on continue.
- **Qu'il exécute git lui-même** — sauf `push`, confirmé à chaque fois.
- **Qu'il rende compte** dans le format fixe → [[rapport-de-tache]].
- **Qu'il propose la suite.** Après avoir pris l'état : recommander les
  prochaines étapes utiles, pas attendre.

## Ce qui va mal quand on ne l'encadre pas

**Le chantier dormant.** Une instance a écrit 5 000 lignes — un module entier —
sans committer, sans tests, sans journal, en citant un ADR qui n'existait pas.
La reprise a coûté une session entière de rétro-ingénierie de nos propres
intentions. → [[ecrire-la-decision-avec-le-code]]

**La reconstruction de l'existant.** Deux fois dans une même session, un agent a
commencé à construire ce qui existait déjà. → [[chercher-avant-d-ecrire]]

**L'affirmation non mesurée.** « Chaque commit compile » écrit dans un message de
commit, sans l'avoir vérifié. C'était faux, et l'affirmation a survécu à
l'erreur. → [[verifier-chaque-commit-du-decoupage]]

**La commande large.** `git add -A docs/` a committé des données sensibles que
l'agent venait lui-même d'écrire qu'il ne fallait pas committer.
→ [[stager-nommement]]

**Le faux diagnostic consigné.** Un défaut inexistant écrit dans le journal
devient une consigne pour l'instance suivante.
→ [[une-conclusion-consignee-devient-consigne]]

## Le dispositif

| Fichier | Effet |
|---|---|
| `~/.claude/CLAUDE.md` | Chargé dans **tous** mes projets : pointe vers ce coffre. |
| `<projet>/CLAUDE.md` | Les règles du projet + la carte de ses docs. |
| `<projet>/JOURNAL.md` | Lu **en premier** à chaque session → [[continuite-entre-sessions]]. |
| `/amorce-projet` | Skill : équipe un dépôt neuf depuis [[amorce-nouveau-projet]]. |
| `/capitaliser` | Skill : fait remonter les leçons du projet vers ce coffre. |
| Sous-agents de revue | Un relecteur « conventions », un relecteur « sécurité », déclenchés selon la zone touchée. |

Détail du câblage : [[obsidian-et-claude]].

## Les sous-agents

Deux valent le coup sur presque tous les projets, définis dans
`<projet>/.claude/agents/` :

- **`code-reviewer`** — à lancer après toute tâche de développement, avant de
  proposer le commit : cohérence avec les conventions du dépôt.
- **`security-reviewer`** — déclenché **proactivement**, même sans demande, dès
  qu'un diff touche l'authentification, les données sensibles, les politiques
  d'accès, ou l'import/export.

Un agent de revue lit ; il ne modifie pas. C'est ce qui le rend utilisable sans
surveillance.

## Ce qu'on ne délègue pas

Le `push`. Le périmètre d'une release. Le choix d'une décision structurante. Et
la lecture du fichier réel avant de modéliser — un export ne se devine pas
depuis ses en-têtes → [[lire-le-fichier-reel-avant-de-modeliser]].
