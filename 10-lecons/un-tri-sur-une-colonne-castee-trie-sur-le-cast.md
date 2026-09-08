---
titre: Un tri sur une colonne castée trie sur le cast
type: lecon
origine: Kalybris — 2026-09-06
tags: [sql, postgres, tri, tests]
---

# Un tri sur une colonne castée trie sur le cast

**Symptôme.** Une chaîne d'intégrité chaînée — chaque entrée scelle la
précédente — se vérifiait correctement pendant des jours, puis a commencé à
échouer sur un journal parfaitement sain. Le message disait « chaînage rompu »
et pointait une entrée dont le lien était pourtant juste.

**Cause.** La requête de vérification :

```sql
SELECT sequence::text, ...
  FROM journal
 WHERE ...
 ORDER BY sequence
```

`sequence::text` produit une **colonne de sortie** nommée `sequence`. Et
PostgreSQL résout `ORDER BY <nom>` sur le nom de **sortie** en priorité, avant
les colonnes de la table. Le tri se faisait donc sur du texte :
`"10" < "11" < "9"`. La chaîne était parcourue dans le désordre.

**Ce qui rend l'affaire mauvaise.** Le défaut n'apparaît **qu'à partir de la
dixième ligne**. En dessous, l'ordre lexicographique et l'ordre numérique
coïncident. Tous les tests écrits jusque-là produisaient moins de dix entrées
et passaient tous — pendant que le code était faux.

**Règle.** Dès qu'une requête caste une colonne dans sa liste de sélection,
**qualifier le `ORDER BY` par la table** : `ORDER BY journal.sequence`. Ou
nommer la sortie autrement. Le même piège vaut pour `GROUP BY` et pour tout
alias qui reprend le nom d'une colonne existante.

**Corollaire de test, qui vaut plus que la règle.** *Un jeu d'essai à un chiffre
ne teste pas un tri.* Tout ce qui dépend d'un ordre — pagination, chaînage,
numérotation de séquence, tri par identifiant — doit avoir au moins un cas qui
**franchit un changement de longueur** : 9→10, 99→100. C'est là, et seulement
là, que l'ordre lexicographique et l'ordre numérique divergent.

**Et une leçon de méthode.** J'ai cherché vingt minutes une contamination entre
tests, en raisonnant sur ce que le code *devrait* faire. Un `SELECT` sur les
données réelles a donné la réponse en dix secondes : elles arrivaient dans
l'ordre 10, 11, 9, et tout était dit. **Regarder la donnée avant de raisonner
sur le code.**

Voir aussi [[mesurer-l-outil-avant-de-conclure]], [[casser-le-test-expres]].
