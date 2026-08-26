---
titre: Poser l'isolation dès le premier schéma
aliases: [Multi-tenant, Cloisonnement]
type: pattern
origine: Synoé — ADR 0001
maj: 2026-08-26
---

# Poser l'isolation dès le premier schéma

**Le principe.** Si le produit pourra un jour servir **plusieurs clients isolés**,
la colonne de cloisonnement existe dès le premier schéma — même s'il n'existe
qu'une seule valeur pendant un an.

**L'arbitrage, chiffré.**

| Moment | Coût |
|---|---|
| Au jour 1 | Une colonne, une politique d'accès. Presque rien. |
| Après des données réelles | Migration, réécriture des requêtes, **et un risque de fuite pendant la transition**. |

**La règle qui va avec.** Ne jamais écrire une requête, une fonction ou un écran
qui **suppose implicitement** qu'il n'y a qu'un seul client — même si c'est vrai
aujourd'hui. C'est cette supposition-là qui coûte cher, pas la colonne.

**Le détail qui mord.** Les politiques d'accès qui doivent consulter une table
pour s'évaluer créent une récursion. Passer par des fonctions dédiées, évaluées
en dehors du jeu de politiques. Et **une politique n'est pas un droit d'accès** :
une table peut être parfaitement protégée et totalement inaccessible
→ [[la-cle-d-administration-ne-va-jamais-cote-client]].

**Ce que l'isolation ne couvre pas.** Le cloisonnement technique ne dit rien du
**besoin d'en connaître** : un rôle légitime dans le système peut n'avoir aucune
raison d'accéder à un contenu donné. Cette règle-là se pose dans le domaine, pas
dans le schéma.

Voir aussi [[isoler-la-persistance-derriere-un-contrat]], [[amorce-nouveau-projet]].
