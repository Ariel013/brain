---
titre: Un budget de poids est une contrainte de périmètre
type: lecon
origine: Kalybris — 2026-09-05
tags: [performance, perimetre, mesure]
---

# Un budget de poids est une contrainte de périmètre

**Symptôme.** Une architecture fixait « budget de bundle : 400 Ko gzip » et
laissait la ligne « à mesurer tôt » ouverte depuis des semaines. Personne ne
savait s'il était tenable — donc personne ne s'en servait pour décider quoi que
ce soit.

**Cause.** Un budget non mesuré n'est pas une contrainte, c'est un vœu. Il ne
tranche aucun arbitrage parce qu'il n'a pas de dénominateur : on ignore ce que
le socle consomme avant la première ligne de code métier.

**Règle.** Mesurer le **socle vide** — le cadre applicatif, la base locale, le
service worker, rien d'autre — avant d'écrire quoi que ce soit. Une demi-heure,
un projet jetable, et un chiffre. C'est ce chiffre qui rend le budget
utilisable.

**Ce que la mesure a produit ici.** Socle vide = 80 Kio, soit **20 % du budget**.
Il restait 320 Kio. Or le prototype à porter pesait 306 Kio minifié pour ses
35 modules, mais **137 Kio pour le seul lot 1**. Autrement dit : tout porter
faisait exploser le budget *avant* le routeur et la synchronisation ; s'en tenir
au lot 1 laissait de la marge.

**La règle sous la règle.** Le budget n'a jamais été une contrainte technique —
c'était une **contrainte de périmètre déguisée**. Et formulée ainsi, elle
convainc : « restons disciplinés sur le lot 1 » est un principe qu'on discute,
« 306 contre 137, sur 320 disponibles » est un arbitrage qu'on tranche. Le même
retournement vaut pour la plupart des budgets de performance : ils ne disent
presque jamais *écris du code plus petit*, ils disent *embarque moins de
choses*.

**Corollaire.** Une fois le chiffre connu, il devient un **test qui échoue en
CI**, pas une ligne qu'on relit en fin de sprint. Sinon il redevient un vœu, et
il faut le remesurer.

Voir aussi [[mesurer-l-outil-avant-de-conclure]],
[[une-release-se-coupe-sur-un-perimetre]].
