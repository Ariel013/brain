---
titre: Un refus partage le prédicat de ce qu'il protège
type: lecon
origine: Synoé — 2026-10-08
tags: [donnees, regles, relecture]
---

# Un refus partage le prédicat de ce qu'il protège

**Symptôme.** Une courbe de biologie trace les mesures liées à une valeur
suivie **par identifiant, ou à défaut par nom** (examens d'avant la liaison).
Le refus de changer l'unité de cette valeur — posé pour empêcher une courbe à
deux unités — ne comptait que les mesures liées **par identifiant**. Sur un
cabinet dont toutes les mesures venaient d'avant, le refus comptait zéro, le
changement passait, et la courbe mêlait g/L et mmol/L sans bruit. L'auteur
ne l'a pas vu ; la relecture oui.

**Cause.** Le refus et la lecture avaient été écrits séparément, chacun avec
son critère « est une mesure de cette valeur ». Deux définitions d'une même
appartenance divergent dès qu'une a un repli que l'autre n'a pas.

**Règle.** Un refus fondé sur « quelque chose le porte » **compte avec le
prédicat exact de la lecture qu'il protège** — une seule fonction exportée
(`estMesureDe`), appelée par la courbe, par le rapprochement à l'écriture
**et** par le refus. Si la lecture a un repli (nom, date approximative,
champ hérité), le refus l'a aussi.

**Corollaire.** Quand on écrit une règle de refus, chercher la lecture
correspondante et lui emprunter son prédicat, jamais le réécrire. Une
relecture utile pose la question : « ce que le refus compte est-il ce que
l'écran montre ? »

Voir aussi [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]],
[[un-seul-etat-derive-le-reste]].
