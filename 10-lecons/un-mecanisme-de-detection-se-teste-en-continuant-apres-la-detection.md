---
titre: Un mécanisme de détection se teste en continuant après la détection
type: lecon
origine: Kalybris — 2026-10-08
tags: [securite, tests, audit]
---

# Un mécanisme de détection se teste en continuant après la détection

**Symptôme.** Un journal d'audit chaîné recevait des « points de contrôle » :
la maintenance scellait chaque jour la dernière entrée de chaque tenant, et
la vérification exigeait que cette entrée existe encore. Testé : on tronque,
on vérifie, l'alerte sonne. Livré.

La recette sur serveur réel a continué une étape de plus : tronquer, vérifier
(l'alerte sonne), **redémarrer le serveur**. La maintenance a posé un nouveau
point sur la nouvelle tête sans regarder le précédent ; la vérification ne
lisait que le dernier point ; l'alerte s'est tue. Un attaquant qui redémarre
le serveur effaçait sa trace. Un second détail du même ordre : un point au
sceau falsifié était « ignoré » — c'est-à-dire que falsifier le point
désactivait la détection.

**Cause.** Le test s'arrêtait au moment gratifiant : celui où l'alerte sonne.
Il n'a jamais laissé tourner ce qui tourne (la maintenance, un redémarrage, le
temps) pour voir si l'alerte tient. Et « ignoré » était un mot rassurant pour
« muet ».

**Règle.**
- *Un test de détection a trois temps, pas deux* : altérer, détecter, **puis
  laisser le système faire son cycle suivant** et vérifier que l'alerte est
  toujours là. Une détection qui ne survit pas au cycle suivant est une
  fenêtre, pas une détection.
- *« Ignoré » n'est jamais un verdict.* Ce qui ne se vérifie pas (sceau faux,
  donnée incohérente) se signale comme une altération ; le silence est la
  réponse d'un mécanisme qui a été contourné.
- *Un mécanisme qui écrit par-dessus son propre état vérifie d'abord cet
  état* : poser un nouveau point ne doit jamais faire disparaître la preuve
  portée par l'ancien.

Voir aussi [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]]
(même journal, la veille) et [[regarder-l-application-fait-partie-de-la-recette]].
