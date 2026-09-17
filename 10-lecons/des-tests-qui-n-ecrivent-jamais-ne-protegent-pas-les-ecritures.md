---
titre: Des tests qui n'écrivent jamais ne protègent pas les écritures
type: lecon
origine: Strongman — 2026-09-16
tags: [tests, base]
---

# Des tests qui n'écrivent jamais ne protègent pas les écritures

**Symptôme.** Trois actions d'écriture plantaient en production — affecter
une catégorie, appeler un athlète, reconstruire une file — sous une suite de
tests à 82/82 au vert.

**Cause.** Les tests couvraient la logique pure : barème, départages, ordre,
lecture des listes. Ils calculaient beaucoup et n'écrivaient rien. Le défaut
était dans la **sérialisation SQL** d'un tableau (`any(${tableau})`, aplati en
paramètres séparés), qu'aucun calcul ne traverse. Pire : deux des trois chemins
ne plantaient qu'au **deuxième** appel, quand le tableau à traiter cessait
d'être vide — un essai manuel rapide les aurait manqués aussi.

**Règle.** Une suite de tests doit **exécuter** les écritures, pas seulement
vérifier ce qui les précède — et les exécuter dans l'état où elles font
vraiment quelque chose : file déjà remplie, plateau déjà occupé. Le cas
intéressant n'est jamais le premier appel sur une base vide.

**Conséquence sur la structure.** Une Server Action qui commence par lire la
session de la requête ne s'exécute pas hors requête, donc pas dans un test.
Ce qui décide de l'état vit donc dans des fonctions ordinaires, et l'action
n'en garde que l'enveloppe : session, journal d'audit, rafraîchissement. Même
famille que [[le-calcul-sort-de-l-ecran]] — ici, l'écriture sort de l'action.

Voir aussi [[casser-le-test-expres]], [[un-test-se-borne-a-son-propre-jeu-de-donnees]].
