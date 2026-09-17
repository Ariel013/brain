---
titre: Un cache « seulement en développement » est un cache absent là où il compte
type: lecon
origine: Strongman — 2026-09-16
tags: [base, performance, production]
---

# Un cache « seulement en développement » est un cache absent là où il compte

**Symptôme.** Les pages mettaient 5 à 8 secondes en production, alors que la
requête SQL elle-même n'était pas lente. En local, rien d'anormal.

**Cause.** Le pool de connexions PostgreSQL était posé sur `globalThis`
**uniquement si `NODE_ENV !== "production"`** — le garde-fou écrit pour
survivre au rechargement des modules en développement. En production, le cache
restait vide et le proxy rouvrait un pool **à chaque accès à une propriété**
de l'objet base. Mesuré : **57 pools ouverts pour 3 requêtes**, autant de
poignées de main TLS.

**Règle.** Un cache de connexion se pose **dans tous les environnements**. Le
besoin du développement (survivre au rechargement des modules) s'ajoute à celui
de la production (ne pas rouvrir la connexion), il ne s'y substitue pas.

**Corollaire.** Une lenteur se **compte** avant d'être expliquée : c'est le
compteur de pools qui a tranché, pas le raisonnement. Voir
[[mesurer-l-outil-avant-de-conclure]].

Voir aussi [[isoler-la-persistance-derriere-un-contrat]], [[verifier-chaque-commit-du-decoupage]].
