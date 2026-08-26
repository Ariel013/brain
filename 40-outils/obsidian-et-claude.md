---
titre: Comment ce coffre est branché à Claude
aliases: [Câblage, Setup]
type: outil
maj: 2026-08-26
---

# Comment ce coffre est branché à Claude

Le coffre vit à `~/PROJETS/brain`. Trois pièces le rendent actif dans **tous**
mes projets, sans que j'aie à l'expliquer.

## 1. Le pointeur global

`~/.claude/CLAUDE.md` est chargé dans **chaque** session Claude Code, quel que
soit le dépôt. Il est volontairement **court** — il ne contient pas la méthode,
il dit où elle est et quand aller la lire. Un fichier global bavard est un
fichier global ignoré.

## 2. `/amorce-projet`

Skill utilisateur (`~/.claude/skills/amorce-projet/`). Sur un dépôt neuf, elle
lit [[amorce-nouveau-projet]], pose les fichiers depuis [[modeles]], et pose les
questions d'amorce qui n'ont pas de réponse évidente dans le dépôt.

Ce qu'elle **ne** fait pas : deviner le domaine. Elle demande, une fois, ce
qu'aucun fichier ne peut lui dire.

## 3. `/capitaliser`

Skill utilisateur (`~/.claude/skills/capitaliser/`). En fin de session, elle lit
les leçons du `JOURNAL.md` du projet courant, repère celles qui **valent au-delà
du projet**, et propose la note à créer ou à enrichir ici — avec ses liens.

Le test d'admission est toujours le même : *est-ce que je voudrais qu'on me le
rappelle sur un projet qui n'a rien à voir ?*

## Ce qui reste dans `~/.claude/`, ce qui vit ici

| Là-bas | Ici |
|---|---|
| Le pointeur global, les skills, les permissions | La méthode, les leçons, les modèles |
| La mémoire auto d'un projet précis | Ce qui vaut pour tous les projets |

La mémoire automatique de Claude et ce coffre ne se concurrencent pas : la
mémoire retient des **faits** courts sur un projet ; le coffre porte la
**méthode**, versionnée, relue, et lisible par moi sans agent.

## Le coffre est un dépôt git

`git init` fait dès le premier jour. Les leçons ont un historique : savoir
**quand** une règle est apparue, et à cause de quoi, fait partie de sa valeur.
Rien de sensible n'entre ici — pas de secrets, pas de données réelles, pas de
noms de personnes.

## Ouvrir le coffre dans Obsidian

Le vault est sous WSL. Depuis Obsidian pour Windows : *Ouvrir un coffre* →
*Ouvrir un dossier existant* → `\\wsl$\Ubuntu\home\password\PROJETS\brain`.
L'indexation initiale est un peu lente sur un chemin réseau ; l'usage ensuite ne
l'est pas.

Voir [[travailler-avec-les-agents]], [[claude-code]].
