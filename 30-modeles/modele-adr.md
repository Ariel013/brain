---
titre: Modèle — ADR
type: modele
cible: docs/decisions/NNNN-<slug>.md
maj: 2026-08-26
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
```

**Le titre est la décision.** « 0002 — Contrat `Repo` : local par défaut,
distant en option » se retrouve dans une liste ; « 0002 — Persistance » non.

**Numérotation continue**, jamais réutilisée. Un ADR remplacé n'est pas
supprimé : son statut change et il pointe vers son successeur. L'historique des
choix abandonnés vaut autant que celui des choix tenus.

Voir [[documents-du-projet]].
