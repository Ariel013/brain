---
titre: Dans une sous-requête écrite à la main, la colonne extérieure se qualifie
type: lecon
origine: Optimisation CV — 2026-10-21
tags: [sql, orm, donnees]
---

# Dans une sous-requête écrite à la main, la colonne extérieure se qualifie

**Symptôme.** Une liste d'entreprises comptait leurs offres par une
sous-requête : `(select count(*) from offres o where o.entreprise_id =
${entreprises.id})`. Le compte valait 1 au lieu de 2, sans erreur.

**Cause.** Dans un `SELECT` sur une seule table, Drizzle écrit la colonne sans
la qualifier : `= "id"`. Dans la sous-requête, SQLite lit `"id"` comme
`o.id`. Dans un `UPDATE`, le même ORM écrit `"offres"."id"` (vérifié par
`toSQL()`) — d'où un code voisin sain et celui-ci faux.

**Règle.** Dans du SQL écrit à la main à l'intérieur d'un ORM, qualifier
explicitement la colonne extérieure (`"entreprises"."id"`), et **lire le SQL
produit** (`toSQL()`) avant de s'y fier. Un test avec deux lignes liées (pas
une) l'aurait vu tout de suite.

Voir [[un-tri-sur-une-colonne-castee-trie-sur-le-cast]], [[un-test-qui-porte-la-formule-la-protege]].
