---
titre: Un verrou se livre avec la voie de correction qui le remplace
type: lecon
origine: Strongman — 2026-09-19
tags: [conception, securite, direct, adr]
---

# Un verrou se livre avec la voie de correction qui le remplace

**Symptôme.** En pleine compétition, devant du public : « il y a une erreur
d'enregistrement sur un athlète, je veux revenir dessus, ce n'est plus
possible. On avait mis cette sécurité. » L'épreuve était terminée, le résultat
validé, et plus aucun bouton ne permettait de le rouvrir.

**Cause.** Deux jours plus tôt, une décision écrite en ADR avait retiré du
plateau toute annulation d'un passage validé — à raison : un résultat déjà lu
sur le mur LED ne doit pas disparaître d'un clic. L'ADR disait que la
correction passerait par un parcours « juge principal » **à venir**, et que
d'ici là la fonction n'était « joignable que par le code ». Le verrou a été
livré ; la voie de remplacement, non. Le besoin est arrivé le jour J, et la
seule personne capable de corriger était celle qui pouvait déployer.

**Règle.** Retirer un geste parce qu'il est dangereux, c'est s'engager à
fournir **dans la même livraison** le geste sûr qui répond au même besoin. Le
besoin ne disparaît pas avec le bouton : une faute de frappe sera validée un
jour. « À venir » dans un ADR de verrou est une dette à échéance inconnue — et
sur un logiciel qui sert un jour par an, l'échéance est ce jour-là.

**Ce que la voie sûre a de différent du geste retiré** (c'est ce qui a été
livré en urgence, et qui aurait dû l'être d'emblée) : elle ne dérange rien
d'autre (le passage ne revient pas au plateau, aucun chrono relancé), elle
**garde et préremplit** l'ancienne valeur au lieu de l'effacer, elle dit avant
de confirmer ce qui change entre-temps, et elle laisse l'ancien résultat
complet au journal d'audit. Corriger n'est pas annuler.

**Le test d'admission d'un verrou.** Avant de le livrer, dérouler à voix haute :
« l'erreur est commise, validée, constatée une heure après — que fait
l'opérateur, seul, sans moi ? » S'il n'y a pas de réponse, le verrou n'est pas
fini.

Voir aussi [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]],
[[ecrire-la-decision-avec-le-code]],
[[une-fonctionnalite-invisible-est-absente]].
