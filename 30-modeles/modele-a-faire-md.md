---
titre: Modèle — A-FAIRE.md
type: modele
cible: A-FAIRE.md
maj: 2026-08-26
---

# Modèle — `A-FAIRE.md`

> Tout ce qui doit être fait **hors code** pour que le projet fonctionne
> réellement. Il complète le backlog de développement, il ne le remplace pas.

```markdown
# À FAIRE — actions manuelles, opérationnelles et externes en attente

Ce fichier recense tout ce qui doit être fait **hors code** : comptes à créer,
secrets à renseigner, migrations à appliquer, décisions produit/juridiques à
trancher, prérequis externes.

> **Règle de tenue :** dès qu'une tâche fait apparaître une action manuelle ou
> externe, elle est ajoutée ici **dans la même tâche**, avec la date. On ne
> laisse aucun prérequis implicite.

Dernière mise à jour : AAAA-MM-JJ.

> 📎 Les **commandes** elles-mêmes sont dans `docs/commandes.md`. Ce fichier-ci
> dit *ce qui reste à faire et pourquoi* ; l'autre dit *comment le lancer*.

---

## 1. Variables d'environnement / secrets

| Variable | Où l'obtenir | Statut |
|---|---|---|
| `<NOM>` | <où> | <requise / en place / optionnelle> |

- ⚠️ Ne jamais committer le fichier d'environnement.

## 2. Comptes / services externes

| Service | Usage | Statut |
|---|---|---|

## 3. Migrations à appliquer

| Migration | Environnement | Statut |
|---|---|---|

## 4. Décisions en attente

| Question | Qui tranche | Échéance | Impact si non tranché |
|---|---|---|---|

## 5. Ops et sauvegardes

- <Ce qui est sauvegardé, à quelle fréquence, et **comment on vérifie**.>
- <Ce qui n'est PAS couvert par la sauvegarde.>
```

Le point 5 mérite une lecture de [[une-sauvegarde-se-verifie-avant-de-detruire]].
