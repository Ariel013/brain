---
titre: Un cache de build restauré peut servir l'ancienne feuille de style ; la mise en ligne se vérifie sur le CSS servi
type: lecon
origine: CV interactif — 2026-10-25
tags: [vercel, nextjs, turbopack, deploiement, verification]
---

# Un cache de build restauré peut servir l'ancienne feuille de style ; la mise en ligne se vérifie sur le CSS servi

**Symptôme.** Un écran de chargement poussé en production apparaissait **sans
aucun style**, et le joystick, déplacé à droite dans le même lot, restait à
gauche. Le HTML était neuf ; la feuille de style servie était celle d'avant :
aucune des nouvelles règles n'y figurait. Le build avait « réussi ». La même
chose s'était produite plus tôt dans la journée en local, après une réécriture
complète de `globals.css` : « Compiled », et l'ancien CSS servi.

**Cause.** Turbopack réutilise son cache `.next`, et Vercel **restaure ce
cache entre deux builds**. Le cache a produit une feuille de style périmée
alors que les composants étaient reconstruits : HTML et CSS de deux versions
différentes, sans aucune erreur.

**Règle.** Un build de production part d'un cache vide quand le style change
beaucoup — ici, `buildCommand: "rm -rf .next && next build"` dans
`vercel.json`, et `rm -rf .next` avant chaque build local de vérification.
Et une mise en ligne qui touche au style se vérifie **sur le CSS servi** :
récupérer les feuilles liées par la page en ligne et y chercher une règle
introduite par le lot. Le statut du déploiement et le HTML neuf ne prouvent
pas que le style suit.

**Corollaire.** Quand un visiteur décrit un écran « moche » ou « pas
changé » juste après une mise en ligne, soupçonner d'abord une version mêlée
avant de retoucher le design.

Voir [[une-fonction-serverless-s-envoie-regroupee-et-se-verifie-au-curl]],
[[regarder-l-application-fait-partie-de-la-recette]],
[[recette-avant-release]].
