---
titre: Modèle — ADR
type: modele
cible: docs/decisions/NNNN-<slug>.md
maj: 2026-11-01
---

# Modèle — ADR (Architecture Decision Record)

> Un ADR se déclenche quand **plusieurs options existaient**. Pas pour acter une
> évidence, pas pour documenter une implémentation. Et il s'écrit **dans le même
> mouvement que le code** → [[ecrire-la-decision-avec-le-code]].

```markdown
# NNNN — <Titre : la décision, pas le sujet>

**Statut** : proposé | adopté | remplacé par NNNN

## Contexte

<Ce qui était vrai au moment de décider, et la contrainte qui forçait un choix.
Écrit pour quelqu'un qui n'était pas là — y compris moi dans six mois.>

## Décision

<Ce qu'on fait. Au présent, à l'affirmatif, sans conditionnel.>

## Pourquoi

- <La raison qui a emporté le choix.>
- <Ce que les autres options coûtaient.>

## Conséquences

- <Ce que ça oblige à faire désormais, systématiquement.>
- <Ce que ça ferme, et ce que ça garde ouvert.>
- <Ce que ça NE résout PAS, dit explicitement.>

## Rapport aux décisions voisines

<Renvois aux ADR liés, et ce qui doit être fait dans le même lot.>
```

**Dire ce que l'ADR ne résout pas** évite qu'une instance suivante croie le
sujet clos. Et quand la décision reformule une demande, **conserver l'énoncé
d'origine** sous un titre « (conservé) » : la reformulation est un choix,
l'énoncé est le fait.

**Le titre est la décision.** « 0002 — Contrat `Repo` : local par défaut,
distant en option » se retrouve dans une liste ; « 0002 — Persistance » non.

**Numérotation continue**, jamais réutilisée. Un ADR remplacé n'est pas
supprimé : son statut change et il pointe vers son successeur. L'historique des
choix abandonnés vaut autant que celui des choix tenus.

Voir [[documents-du-projet]].
