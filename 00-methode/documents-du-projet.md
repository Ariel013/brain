---
titre: Les documents d'un projet
aliases: [Documents du projet, Carte des docs]
type: methode
maj: 2026-08-26
---

# Les documents d'un projet

Chaque document répond à **une question, et une seule**. Le jour où deux
documents répondent à la même, l'un des deux prend du retard et devient un
piège. C'est la même mécanique que [[une-enumeration-de-champs-se-teste]] :
toute information recopiée à un second endroit finit par diverger.

## La carte

| Document | Question à laquelle il répond | Lu par |
|---|---|---|
| `CLAUDE.md` | *Quelles sont les règles, et quel doc lire pour quel sujet ?* | l'agent, à chaque session |
| `JOURNAL.md` | *Où en est-on, quoi faire ensuite, quoi éviter ?* | l'agent, en premier |
| `A-FAIRE.md` | *Que reste-t-il à faire **hors code** ?* | moi + l'agent |
| `docs/architecture.md` | *Comment c'est fait, et **pourquoi** comme ça ?* | avant toute décision structurante |
| `docs/decisions/NNNN-*.md` | *Pourquoi ce choix plutôt qu'un autre ?* (ADR) | avant de remettre un choix en cause |
| `docs/conventions-code.md` | *À quoi doit ressembler le code que j'écris ?* | avant de coder |
| `docs/workflow-git.md` | *Comment on branche, commit, promeut, tague ?* | avant tout commit |
| `docs/commandes.md` | *Comment je lance ça ?* (et **ce qu'il ne faut jamais lancer**) | moi, en usage |
| `docs/roadmap-backlog.md` | *Que reste-t-il à construire, dans quel ordre ?* | au démarrage de session |
| `docs/points-avancement.md` | *Qu'est-ce qui change pour l'utilisateur ?* | l'utilisateur final |

## Les trois qu'on oublie, et ce que ça coûte

**`A-FAIRE.md`** — sans lui, les prérequis externes (un secret à renseigner, une
migration à appliquer, une décision juridique) vivent dans une conversation et
meurent avec elle. Règle de tenue : dès qu'une tâche fait apparaître une action
manuelle, elle est ajoutée **dans la même tâche**, datée.

**`docs/commandes.md`** — l'aide-mémoire de toutes les commandes, avec un
marquage explicite de celles qui sont **destructives ou touchent des données
réelles**. Sa vraie valeur est là : dire ce qu'il ne faut *jamais* lancer.

**`docs/points-avancement.md`** — le seul document écrit pour l'utilisateur
final. Quatre sections, toujours les mêmes :
1. **Ce qui change pour vous** — l'effet concret sur le travail quotidien.
2. **Ce qui était cassé** — nommé sans détour, *y compris ce que personne
   n'avait vu*.
3. **Ce qui reste ouvert** — et pourquoi.
4. **Ce qu'on attend de vous** — les vérifications et décisions qui reviennent
   à l'utilisateur, sous forme de marche à suivre exécutable.

Modèle : [[modele-point-avancement]]. Une marche à suivre qui **suppose** un état
préalable est intestable : elle doit le fabriquer elle-même à l'étape 1
→ [[une-fonctionnalite-invisible-est-absente]].

## Les ADR

Un ADR se déclenche quand **plusieurs options existaient**. Pas pour acter
l'évidence, pas pour documenter une implémentation. Format en cinq blocs :
titre numéroté, statut, contexte, décision, pourquoi, conséquences.
Voir [[modele-adr]].

La règle qui compte : **l'ADR s'écrit dans le même mouvement que le code qui
l'applique**, jamais après. → [[ecrire-la-decision-avec-le-code]]

## Tenue à jour

Un document se met à jour **dans la tâche qui le rend faux**, pas dans une
« passe de doc » ultérieure qui n'arrive jamais. Et quand une tâche fait
apparaître une convention durable, elle s'écrit dans `conventions-code.md`
tout de suite — sinon elle reste implicite dans le code seul, où personne ne
la lira.
