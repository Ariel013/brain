---
titre: Regarder l'application fait partie de la recette
type: lecon
origine: Synoé — 2026-08-23
tags: [recette, tests]
---

# Regarder l'application fait partie de la recette

**Symptôme.** 480 tests verts, un build vert, un typecheck vert — et **trois
écrans qui ne s'affichaient pas**. Ils seraient partis en production.

**Cause.** Des tests ne prouvent que ce qu'ils exercent. Aucun n'ouvrait un
écran.

**Règle.** Avant toute release, **ouvrir chaque écran touché**. La première passe
visuelle a trouvé le défaut en quatre minutes.

**Automatisable sans rien installer :** un fichier d'environnement gitignoré qui
force le mode local, un second serveur de dev sur un autre port pour ne pas
déranger celui qui tourne, puis une capture par route en navigateur sans
interface. Aucun identifiant, aucune donnée réelle, aucune interaction — mais un
écran mort se voit immédiatement.

**Corollaire.** Balayer **plusieurs largeurs**, pas seulement la plus grande.

Voir aussi [[recette-avant-release]], [[mesurer-l-outil-avant-de-conclure]],
[[une-propriete-de-colonne-ne-survit-pas-a-une-rangee]].
