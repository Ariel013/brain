---
titre: Deux états qui doivent toujours s'accorder sont un seul état mal nommé
type: lecon
origine: Synoé — 2026-08-23
tags: [architecture, etat]
---

# Deux états qui doivent toujours s'accorder sont un seul état mal nommé

**Symptôme.** Un agenda portait « le mois affiché » **et** « le jour choisi ».
Les flèches déplaçaient le premier, la vue semaine lisait le second : en vue
semaine, les flèches ne faisaient rien. Trois endroits du code existaient
uniquement pour resynchroniser les deux — et ne couvraient pas tous les chemins.

**Cause.** Le défaut n'était pas dans les flèches, il était **dans le modèle**.

**Règle.** Quand deux morceaux d'état doivent **toujours** rester cohérents,
n'en garder qu'un et **dériver** l'autre.

**Le symptôme à guetter :** du code dont le seul rôle est de recopier une valeur
dans une autre après chaque action. Chaque resynchronisation est un aveu.

Voir aussi [[un-selecteur-lit-il-ne-calcule-pas]], [[une-enumeration-de-champs-se-teste]].
