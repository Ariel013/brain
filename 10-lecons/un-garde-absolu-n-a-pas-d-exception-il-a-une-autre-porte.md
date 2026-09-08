---
titre: Un garde absolu n'a pas d'exception, il a une autre porte
type: lecon
origine: Kalybris — 2026-09-06
tags: [securite, conception, base-de-donnees]
---

# Un garde absolu n'a pas d'exception, il a une autre porte

**Symptôme.** Un journal d'audit avait été rendu **append-only sans
condition** : droits révoqués sur le rôle applicatif, et un trigger de base qui
refuse `UPDATE` et `DELETE` y compris à un superutilisateur. C'était le but, et
c'était vérifié par des tests.

Puis est venue la rétention. Un journal doit finir par oublier — sinon il
grossit sans fin. Et là, plus rien ne pouvait supprimer une ligne.

**La mauvaise réponse, qui vient en premier.** Ajouter une condition au
trigger : « refuse, sauf si telle variable de session est posée », ou désactiver
le trigger le temps de la purge. Les deux reviennent au même : **un garde-fou
avec une exception n'est plus un garde-fou, c'est un garde-fou avec une porte.**
Une porte finit par être empruntée — par un script de maintenance recopié, par
quelqu'un qui débogue un dimanche — et le jour où elle l'est, personne ne le
sait, puisque c'est précisément le journal qui aurait dû le dire.

**La bonne réponse : changer de niveau.** La table a été **partitionnée par
mois**. Purger, c'est alors supprimer une partition, c'est-à-dire du **DDL** —
et un trigger de ligne ne se déclenche pas sur du DDL. L'immuabilité au niveau
des lignes reste absolue, sans condition, sans variable, sans exception. Et la
suppression exige d'être propriétaire de la table : l'application, elle, ne peut
toujours rien effacer.

**Règle.** Quand un garde absolu empêche une opération légitime, **ne pas
l'affaiblir** : chercher une opération qui atteint le même but à un autre
niveau, où le garde ne s'applique pas parce qu'il n'a pas à s'appliquer. Si on
n'en trouve pas, c'est alors seulement qu'il faut rediscuter le garde — en
plein jour, pas dans une clause `IF`.

**Le test qui dit qu'on a bien fait.** Après le changement, la tentative
d'`UPDATE` et de `DELETE` en superutilisateur doit **toujours** échouer. Si
elle passe, on a déplacé la porte, pas supprimé le besoin.

**Corollaire de conception.** Une opération destructrice se découpe en deux
temps séparés par un **mur de droits**, pas par une convention d'appel : ici,
l'application prépare (elle pose les ancres qui garderont le journal
vérifiable), et seul l'exploitant supprime. Une interruption entre les deux
laisse alors un état sain, jamais un état intermédiaire dangereux.

Voir aussi [[une-sauvegarde-se-verifie-avant-de-detruire]],
[[un-garde-fou-trop-large-empeche-sa-propre-documentation]],
[[la-cle-d-administration-ne-va-jamais-cote-client]].
