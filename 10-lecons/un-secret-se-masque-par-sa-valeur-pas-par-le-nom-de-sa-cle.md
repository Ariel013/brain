---
titre: Un secret se masque par sa valeur, pas par le nom de sa clé
type: lecon
origine: outillage Claude Code — 2026-11-20
tags: [securite, outillage]
---

# Un secret se masque par sa valeur, pas par le nom de sa clé

**Symptôme.** Pour retirer un serveur MCP, sa configuration a été affichée avec
un filtre censé masquer les secrets (`sed` sur `x-api-key` et `Authorization`).
La clé est sortie en clair dans la transcription : elle était rangée sous
`env.API_KEY`, un nom que le filtre ne prévoyait pas.

**Cause.** Le masquage reposait sur une **liste de noms de clés devinée
d'avance**. Chaque outil range ses secrets sous un nom différent (`API_KEY`,
`token`, `apiKey`, `SUPABASE_SERVICE_ROLE_KEY`, une URL avec mot de passe…) : la
liste a toujours un trou, et le trou ne se voit qu'une fois le secret affiché.

**Règle.** Pour inspecter une configuration, **afficher la structure, pas les
valeurs** : les noms de clés et les types seulement, ou toutes les valeurs de
`env`, `headers` et des URL remplacées par `***`. On regarde une valeur précise
seulement quand on en a besoin, et après s'être assuré qu'elle n'est pas
secrète.

**Corollaire.** Un secret affiché une fois l'est pour de bon (transcription,
historique, journaux) : s'il était valide, il se **renouvelle**, il ne
s'efface pas.

Voir aussi [[la-cle-d-administration-ne-va-jamais-cote-client]],
[[un-env-ne-se-source-pas-dans-le-shell]].
