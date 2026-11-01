---
titre: Un jeu de démonstration se teste comme une fixture
type: lecon
origine: Synoé, 2026-08
tags: [tests, donnees]
---

# Un jeu de démonstration se teste comme une fixture

**Symptôme.** Deux effets opposés, tous les deux coûteux. Un champ que personne
n'écrivait a paru fonctionner pendant des semaines, parce que les données de
démo le portaient. Et à l'inverse, les courbes n'apparaissaient nulle part dans
la démonstration, parce que les données de démo ne portaient aucune constante.

**Cause.** Le jeu de démonstration avait divergé du modèle, en silence. Rien ne
vérifiait qu'il exerçait ce que l'application sait montrer.

**Règle.** Un jeu de démo est une fixture, pas un décor. Un test vérifie qu'il
exerce **chaque fonctionnalité visible**, et il se met à jour **dans la même
tâche que le modèle**.

Voir aussi [[verifier-le-chemin-d-ecriture]], [[conventions-de-code]].
