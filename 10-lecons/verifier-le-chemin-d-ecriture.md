---
titre: Vérifier le chemin d'écriture, pas l'écran
type: lecon
origine: Synoé — 2026-08-25 et 2026-08-22
tags: [donnees, tests]
---

# Vérifier le chemin d'écriture, pas l'écran

**Symptôme.** Une fonctionnalité marchait : elle apprenait, proposait, les tests
passaient. Elle n'était simplement **jamais écrite** — la seule fonction de
persistance ne listait pas sa clé. Aucune erreur, aucun test rouge : la donnée
disparaissait au rechargement. Deux jours en production.

Variante, plus ancienne : un champ s'affichait dans trois écrans et déclenchait
des alertes. Tout venait du jeu de démonstration ; **aucun écran ne l'écrivait**.
Un champ que personne n'écrit n'est pas un modèle, c'est un décor.

**Cause.** On vérifie ce qu'on voit. Une lecture réussie ne dit rien de
l'écriture, et un jeu de démo fournit des lectures parfaitement crédibles.

**Règle.** **Toute nouvelle clé d'état se vérifie sur le chemin d'écriture.**
Avant de faire évoluer un modèle, chercher **son chemin d'écriture**, pas ses
lectures.

**Le patron qui l'attrape.** Un jeu d'essai typé `Record<keyof État, unknown>` —
le compilateur refuse alors d'oublier une clé — plus un test qui compare les
clés effectivement écrites aux clés attendues et **nomme** la manquante.

Voir aussi [[une-enumeration-de-champs-se-teste]], [[casser-le-test-expres]],
[[chercher-avant-d-ecrire]].
