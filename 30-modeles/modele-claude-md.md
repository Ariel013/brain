---
titre: Modèle — CLAUDE.md
type: modele
cible: CLAUDE.md
maj: 2026-10-21
---

# Modèle — `CLAUDE.md`

> Le fichier lu à **chaque** session. Il ne raconte pas le projet : il dit les
> règles et **quel doc lire pour quel sujet**. Court, sinon il n'est pas suivi.

```markdown
# <Projet> — contexte projet pour Claude Code

Lis ce fichier en entier avant toute tâche. Il pointe vers les docs de
référence — lis aussi celles qui concernent ta tâche avant de coder.

> **⚡ EN TOUT PREMIER, à chaque nouvelle session : lis `JOURNAL.md`.**
> C'est le fil de continuité (où on en est, la prochaine action, les leçons
> apprises). Tu le **mets à jour en fin de session**.

## Le projet en une phrase

<Ce que c'est, pour qui, à quel stade.>

## Où en est le projet — LIS CECI AVANT TOUTE CHOSE

- **Phase actuelle : <…>.** <Ce qu'il ne faut pas supposer déjà en place.>
- <Ce qui est volontairement mis de côté, et où c'est décidé.>
- <Ce qui n'est pas encore câblé, et sous quelle contrainte le faire.>

## Stack technique

- <Frontend / backend / persistance / hébergement, en une ligne chacun.>

## Documents de référence — à consulter selon la tâche

| Doc | Quand le lire |
|---|---|
| `JOURNAL.md` | **En tout premier, à chaque session.** |
| `A-FAIRE.md` | Pour les actions manuelles/externes en attente |
| `docs/architecture.md` | Avant toute décision structurante |
| `docs/conventions-code.md` | Avant d'écrire du code |
| `docs/workflow-git.md` | Avant tout commit |
| `docs/commandes.md` | Aide-mémoire des commandes — et de celles à ne jamais lancer |
| `docs/decisions/` | Avant de remettre en cause un choix déjà fait |
| `docs/roadmap-backlog.md` | Au démarrage de chaque session |

## Règles d'or, non négociables

1. **Ne jamais faire `git push` sans confirmation explicite, à chaque fois.**
2. <La règle d'isolation / de sécurité propre au domaine.>
3. **Sur une décision d'architecture ambiguë, s'arrêter et demander** plutôt
   que d'improviser silencieusement.
4. <La règle métier qui prime sur tout le reste.>
5. <Les contraintes techniques déjà posées — dépendances interdites, etc.>

## Après chaque tâche — format de rapport attendu

Tout retour de l'agent — rapport de fin de tâche ou réponse en cours de
session — donne **l'utile seulement** (format du coffre,
`brain/00-methode/rapport-de-tache.md`, revu le 2026-10-20) :

​```
## <la tâche en une ligne>
**Fait** : actions effectuées et résultat mesuré ; ce qui reste non vérifié
**Sécurité** : revue du diff faite → constats ; ou non faite → pourquoi
**Challenge** : ce que je remets en cause dans ce qui est proposé ou à faire, et ma recommandation
**À toi** : décisions à prendre, actions manuelles, dans l'ordre
**Commit proposé** : <message exact, non encore exécuté>
​```

Pas de liste de fichiers, pas de code, pas de commandes, pas de compte rendu
brut de sous-agent : l'agent les vérifie et ne les remonte que s'ils changent
une décision. Un changement de schéma, d'auth, de données sensibles ou une
décision qui mériterait un ADR se signale toujours, en une ligne.

L'utilisateur valide le commit avant qu'il ne soit fait.

## Continuité entre sessions

1. **Reprise sans relecture du code** : `JOURNAL.md` + ce fichier suffisent.
2. **Apprendre des erreurs** : toute erreur corrigée est consignée dans
   « Leçons apprises » de `JOURNAL.md`.
3. **Être force de proposition** : après avoir pris l'état, recommander la
   suite — ne pas lister des options.

En fin de session, mettre à jour `JOURNAL.md`. C'est la condition de la reprise.
```

Voir [[documents-du-projet]], [[rapport-de-tache]], [[travailler-avec-les-agents]].
