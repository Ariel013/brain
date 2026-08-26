---
titre: Amorcer un nouveau projet
aliases: [Amorce, Amorce nouveau projet]
type: methode
maj: 2026-08-26
---

# Amorcer un nouveau projet

> **Note maîtresse.** C'est elle que lit l'agent au premier jour d'un dépôt.
> Elle dit ce qui doit exister **avant la première ligne de code**, et dans
> quel ordre.

## Le principe

Un projet ne commence pas par du code, il commence par **sa discipline**. Les
fichiers ci-dessous ne sont pas de la paperasse : chacun existe parce que son
absence a déjà coûté cher (voir [[lecons]]). Les poser prend vingt minutes ; les
poser après coup en prend dix fois plus, quand la mémoire des intentions est
déjà partie.

## Étape 1 — Les cinq fichiers d'amorce

À la racine du dépôt, dans cet ordre :

| Fichier | Rôle | Modèle |
|---|---|---|
| `CLAUDE.md` | Les règles non négociables + la carte des docs. Lu à chaque session. | [[modele-claude-md]] |
| `JOURNAL.md` | Le fil de continuité entre sessions : état, prochaine action, leçons. | [[modele-journal-md]] |
| `A-FAIRE.md` | Ce qui doit être fait **hors code** : comptes, secrets, migrations, décisions. | [[modele-a-faire-md]] |
| `README.md` | Ce qu'est le projet, pour un humain qui arrive. | — |
| `docs/decisions/` | Les ADR. Vide au départ, mais **le dossier existe** : sa présence appelle son usage. | [[modele-adr]] |

Puis, dès que le sujet apparaît (pas avant — un doc vide qui ment est pire que
pas de doc) :

`docs/architecture.md`, `docs/conventions-code.md`, `docs/workflow-git.md`,
`docs/commandes.md`, `docs/roadmap-backlog.md`, `docs/points-avancement.md`.
Leur rôle respectif est décrit dans [[documents-du-projet]].

## Étape 2 — Les questions à trancher tout de suite

Ces choix coûtent presque rien le premier jour et très cher au centième. Les
poser en ADR **même si la réponse semble évidente** : c'est le *pourquoi* qu'on
perd, pas le *quoi*.

1. **Isolation / multi-tenant.** Si le produit pourra un jour servir plusieurs
   clients isolés, la colonne de cloisonnement existe **dès le premier schéma**,
   même s'il n'y a qu'une valeur. → [[poser-l-isolation-des-le-premier-schema]]
2. **Où vivent les données, et qui peut les lire.** Local, distant, les deux ?
   Derrière quel contrat ? → [[isoler-la-persistance-derriere-un-contrat]]
3. **Langue du domaine.** Le vocabulaire métier se choisit une fois et ne
   bascule jamais à mi-projet. → [[conventions-de-code]]
4. **Discipline de migration.** Avant la première donnée réelle, un dossier de
   migrations additives. Un `drop table` ré-exécutable est une bombe à retardement
   dès qu'un utilisateur saisit quelque chose.
5. **Ce que le projet ne fera pas.** Écrit noir sur blanc. Un hors-périmètre
   explicite évite le sur-développement mieux qu'un backlog bien rangé.

## Étape 3 — Les garde-fous techniques

- **Branches** : `main` ← `staging` ← `dev` ← `<type>/<slug>`. Détail et
  justification dans [[workflow-git]].
- **Hook `pre-push` local** qui refuse force-push et suppression sur les
  branches longues — la protection serveur n'est pas toujours disponible.
- **CI** dès le premier commit : typecheck + tests + build sur `dev`.
- **`.gitignore` avant le premier `git add`**, et jamais de stage en masse
  → [[stager-nommement]].

## Étape 4 — Ce que l'agent doit savoir de moi

Ces préférences sont durables, elles n'ont pas à être redites :

- Je veux qu'on **exécute** les commandes git — sauf `git push`, qui demande une
  confirmation explicite **à chaque fois**, jamais acquise une bonne fois.
- Je veux qu'on **tranche** les choix techniques ordinaires plutôt que de me
  soumettre une liste d'options. En revanche un choix **structurant** ambigu
  s'arrête et se pose. → [[rapport-de-tache]]
- Je veux un **rapport de tâche** avant tout commit, dans un format fixe.
- Je veux des points d'avancement **écrits pour l'utilisateur final**, pas pour
  un développeur. → [[documents-du-projet]]
- Je travaille en **français**, y compris dans le code du domaine et les docs.
- **Une seule copie de travail sous le serveur de dev.** Pour tout ce qui
  demande une autre branche : un worktree jetable. → [[verifier-chaque-commit-du-decoupage]]

## Étape 5 — Avant de coder quoi que ce soit

Lire [[lecons]]. Ce n'est pas une formalité : la moitié de ces règles ont été
payées par un défaut parti en production.

## Comment cette note s'améliore

Chaque projet qui découvre un prérequis manquant l'ajoute **ici**, dans la même
session. Si une étape s'est révélée inutile deux projets de suite, elle se
retire. Voir [[continuite-entre-sessions]].
