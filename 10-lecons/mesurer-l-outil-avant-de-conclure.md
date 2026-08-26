---
titre: Un outil de mesure se mesure avant de conclure
type: lecon
origine: Synoé — 2026-08-24
tags: [methode, recette]
---

# Un outil de mesure se mesure avant de conclure

**Symptôme.** Un défaut a été consigné dans le journal du projet — « les écrans
débordent sous 440 px » — sur la foi de captures d'écran. Le défaut **n'existait
pas**.

**Cause.** Le navigateur sans interface **plafonne la fenêtre à 500 px** : en
dessous, il rend la page à 500 px et **rogne** l'image à la taille demandée. Une
capture rognée est visuellement indiscernable d'un débordement.

**Règle.** **Une observation faite à travers un outil ne vaut que si l'outil a
été vérifié dans le régime où on l'emploie.** Avant de conclure, demander à la
source ce qu'elle voit (ici : `innerWidth`, `scrollWidth`) plutôt que de croire
l'image.

Et une mesure **au-delà des limites de l'outil** se fait autrement : ici, un
cadre de la largeur voulue dans une fenêtre restée au-dessus du plancher — il
mesure *et* photographie juste.

**Corollaire, plus gênant.** Le faux défaut avait été écrit dans le journal, donc
dans la mémoire du projet. → [[une-conclusion-consignee-devient-consigne]]

Voir aussi [[regarder-l-application-fait-partie-de-la-recette]].
