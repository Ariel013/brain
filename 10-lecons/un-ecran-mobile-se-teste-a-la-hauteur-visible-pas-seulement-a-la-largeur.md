---
titre: Un écran mobile se teste à la hauteur visible, pas seulement à la largeur
type: lecon
origine: cv-interactif — 2026-10-31
tags: [front, mobile, responsive, recette]
---

# Un écran mobile se teste à la hauteur visible, pas seulement à la largeur

**Symptôme.** Écran titre d'un CV web (nom, titre, pastilles, accroche,
quatre boutons). Un lot précédent l'avait « vérifié sans débordement à 320,
360 et 390 px », et la session du jour l'avait encore capturé à 320 × 700 :
tout tenait. Kevin demande que la version téléphone « fit ». Mesuré à
320 × 568 : 642 px de contenu pour 502 px visibles, l'écran titre défile et
la ligne du bas est coupée.

**Cause.** Les tailles de test étaient choisies par la largeur, avec une
hauteur confortable laissée au hasard. Sur un vrai téléphone, la hauteur
utile est l'écran moins les barres du navigateur (≈ 548 px sur un iPhone SE
dans Safari), moins l'en-tête du site. Le débordement vertical ne se voit pas
sur une capture faite trop haute, et un conteneur qui défile en lui-même
(`overflow-y: auto`) ne casse rien : il cache le défaut.

**Règle.** Un écran qui doit tenir sans défiler se mesure **à la hauteur
visible réelle** : 320 × 548, 360 × 560, 375 × 548, 390 × 664, et chaque
langue. Mesurer, pas regarder : `scrollHeight` contre `clientHeight` du
conteneur, `scrollWidth` du document pour la largeur.

**Corollaire.** Pour le faire tenir, une requête `max-height` qui resserre
marges, pastilles et boutons, plutôt que retirer un contenu choisi
(ici les modalités d'alternance, mises en avant exprès).

Liens : [[regarder-l-application-fait-partie-de-la-recette]],
[[une-propriete-de-colonne-ne-survit-pas-a-une-rangee]],
[[un-champ-qui-ne-s-envoie-qu-avec-entree-est-bloque-sur-telephone]]
