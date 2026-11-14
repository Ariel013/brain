---
titre: Une sortie vérifiée ne se remplace que par une sortie vérifiée
type: lecon
origine: Optimisation CV — 2026-11-12
tags: [donnees, regeneration, verification]
---

# Une sortie vérifiée ne se remplace que par une sortie vérifiée

**Symptôme.** Un lot refaisait les PDF de 32 candidatures en cours pour y
reporter une nouvelle ligne de contact. Plusieurs générations tournaient en
même temps ; certaines ont échoué (`spawnSync google-chrome ETIMEDOUT`,
PDF de deux pages). Le lot signalait bien « refusé »… mais les PDF d'origine,
vérifiés et bons, avaient déjà été écrasés par les sorties refusées.

**Cause.** Le générateur écrivait au même nom que l'original : la vérification
venait **après** l'écriture. Un refus disait que la nouvelle sortie était
mauvaise, sans rien rendre de l'ancienne. Et sous charge, l'outil de rendu
(Chrome sans interface) produit des sorties qu'il ne produit pas seul.

**Règle.** Refaire une sortie déjà vérifiée se fait **à côté** : sous un nom
d'essai, vérifiée, puis renommée sur l'original seulement si elle passe ;
l'essai est supprimé dans tous les cas. Une variante refusée garde l'ancienne
variante vérifiée. Le refus devient alors sans dommage, et le lot peut être
relancé.

**Corollaire.** Un lot qui fait tourner un outil lourd en parallèle se mesure
aussi seul : un échec sous charge n'est pas un défaut du contenu (ici, relancées
une par une, toutes passaient).

Voir [[refaire-depuis-une-copie-figee-ne-reprend-pas-la-source]], [[une-sauvegarde-se-verifie-avant-de-detruire]], [[un-lot-qui-ecrit-sur-les-vraies-donnees-s-essaie-sur-un-seul-element]].
