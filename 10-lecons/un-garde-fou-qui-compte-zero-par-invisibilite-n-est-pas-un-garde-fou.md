---
titre: Un garde-fou qui compte zéro par invisibilité n'est pas un garde-fou
type: lecon
origine: Kalybris — 2026-10-07
tags: [securite, base-de-donnees, tests, droits]
---

# Un garde-fou qui compte zéro par invisibilité n'est pas un garde-fou

**Symptôme.** Une purge de journal d'audit refusait de supprimer une partition
tant qu'une officine n'avait pas son ancre : « compte les officines sans ancre ;
si > 0, refuse ». Testé, vert, documenté. En production, sous le rôle réel
(propriétaire du schéma, non superutilisateur), la sécurité par ligne (RLS)
sans tenant posé rendait **zéro ligne**. Zéro officine visible, donc zéro
officine sans ancre, donc purge autorisée — et la partition partait avec les
sceaux de toutes les officines. Chaîne rompue, définitivement, sans erreur.

Le matin même, un correctif voisin avait **documenté** ce comportement
(« sous ce rôle, ce chemin ne rend rien ») sans en tirer la conséquence.
Décrire un trou n'est pas le fermer.

**Cause.** Deux choses, qui se cumulent.

1. Le garde-fou raisonnait sur ce qu'il *voyait* comme si c'était ce qui
   *existait*. Un compteur qui peut valoir zéro parce qu'on ne voit rien est
   indistinguable d'un compteur qui vaut zéro parce que tout va bien.
2. Les tests tournaient en **superutilisateur**, qui ignore la RLS, les droits
   d'exécution et les triggers. Toute une classe de défauts — ceux qui
   dépendent de *qui* exécute — était invisible par construction. Les tests
   prouvaient le code, pas le code sous le rôle qui le fera tourner.

**Règle, en trois parties.**

- *Un garde-fou vérifie d'abord qu'il voit.* S'il dépend d'une vue sur les
  données, il refuse quand il n'a pas cette vue, au lieu de conclure que rien
  ne manque. En SQL : `IF NOT pg_has_role(current_user, 'rôle_de_vue') THEN
  RAISE`.
- *Une vue élargie s'obtient par une politique nommée, jamais par le hasard du
  rôle de connexion.* Un rôle dédié, une policy qu'on peut lire dans le schéma,
  un `SET LOCAL ROLE` explicite dans le code. Le privilège d'un
  superutilisateur « qui voit tout » n'est pas une conception, c'est un
  accident qui marche.
- *Au moins un fichier de tests tourne sous le rôle de production.* Un rôle
  non privilégié, propriétaire d'une base qu'il migre lui-même, et dessus tout
  ce qui touche aux droits, à la maintenance, aux triggers. C'est le test qui
  aurait attrapé le défaut, et c'est le seul qui le pouvait.

**Le test qui dit qu'on a bien fait.** Sous le rôle de production, deux
tenants avec des données anciennes, une purge : une ancre **par tenant**, la
partition supprimée, chaque chaîne vérifiable. Et sous un rôle sans la vue :
la purge **refuse**, elle ne réussit pas en silence.

Voir aussi [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]] (même
journal, l'épisode précédent) et
[[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]].
