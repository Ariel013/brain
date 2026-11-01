---
titre: Modèle — JOURNAL.md
type: modele
cible: JOURNAL.md
maj: 2026-11-01
---

# Modèle — `JOURNAL.md`

> Le fil de continuité. Il **oriente**, il ne duplique pas les docs spécialisés :
> il y renvoie. Dates toujours absolues.

```markdown
# 🧭 Journal de bord — <Projet>

> **Nouvelle session : LIS CE FICHIER EN PREMIER**, puis `CLAUDE.md`. Tu sauras
> où on en est, quoi faire ensuite et quoi éviter — sans relire tout le code.
>
> **Discipline** :
> 1. Au **démarrage** : lire les trois sections ci-dessous, puis agir / proposer.
> 2. En **fin de session** : mettre à jour « État & prochaine action », ajouter
>    une entrée au journal des sessions, consigner toute erreur en « Leçons ».
> 3. Convertir les dates relatives en absolues. Rester concis.

Carte des documents : <liste courte, avec ce que chacun répond.>

---

## 📍 État actuel & prochaine action

*(Mis à jour le AAAA-MM-JJ.)*

- **Version en prod** : <version>, déploiement **vérifié** le <date> — <par quoi
  il a été vérifié : bundle servi, routes, contenu réellement téléchargé>.
- **État des branches** : <alignées avec origin, vérifié par SHA / divergence
  connue et pourquoi ce n'en est pas une>.
- **Recette au <date>** : <n tests, typecheck, build, passe visuelle>.
- **Prochaine action** : <une seule, la plus utile, avec son critère de fin.>
- **En attente côté utilisateur** (l'agent ne peut pas le faire) : <…>

## 📓 Journal des sessions (plus récent en haut)

### AAAA-MM-JJ — <titre qui dit ce qu'on a appris, pas ce qu'on a fait>
<Ce qui a été fait, décidé, découvert. Ce qui reste ouvert. Ce qui n'a pas pu
être vérifié, et pourquoi.>

## 🎓 Leçons apprises

*Une entrée dès qu'une erreur est commise et corrigée. Format : symptôme →
cause → règle. Ce qui vaut au-delà de ce projet monte dans le brain.*

### <La règle, énoncée comme un titre> (AAAA-MM-JJ)
<Symptôme tel qu'il s'est présenté.>
<Cause réelle.>
Règle : <ce qu'on fait désormais.>
```

Au-delà d'environ 300 lignes, les sessions anciennes partent dans
`docs/journal-archive-AAAA-MM.md` → [[continuite-entre-sessions]].

Voir [[continuite-entre-sessions]], [[lecons]].
