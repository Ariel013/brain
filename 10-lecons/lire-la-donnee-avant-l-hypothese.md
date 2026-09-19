---
titre: Devant un résultat surprenant, lire la donnée avant le code — et avant l'hypothèse
type: lecon
origine: Strongman — 2026-09-17 et 2026-09-20
tags: [diagnostic, donnees, utilisateur]
---

# Devant un résultat surprenant, lire la donnée avant le code — et avant l'hypothèse

**Symptôme.** Deux fois sur le même projet, un rapport d'utilisateur est arrivé
avec son diagnostic. « Le niveau ne passe pas, le select ne prend pas » — donc
un bug d'enregistrement. Puis : « j'ai mis zéro à tout le monde et ça a calculé
des points, c'est parce que je n'ai pas mis les 90 secondes » — donc un bug de
chronomètre.

**Cause.** Aucune des deux hypothèses n'était la bonne, et le code n'était en
défaut là où on l'attendait dans aucun des deux cas. La première fois, la base
disait `niveau = true, options = null` : un sélecteur sans option, rien à
enregistrer. La seconde, elle disait 21 lignes `ok · valeur 0` : des « 0 »
saisis comme **performances**, pas le verdict Zéro — classées, à égalité,
départagées au poids de corps. Dans les deux cas **une seule requête en
lecture** a donné la cause en une minute ; partir du code, ou de l'hypothèse
fournie, aurait mené au mauvais module.

**Règle.** Un rapport décrit un **effet** et propose une **cause** : on garde
l'effet, on met la cause de côté. Premier geste : lire en base les lignes
exactes dont parle l'utilisateur. Ensuite seulement, le code — et uniquement
celui que la donnée désigne. L'hypothèse de l'utilisateur se traite à la fin,
explicitement : « ce n'était pas les 90 secondes, voici pourquoi » — sinon il
la gardera.

**Corollaire.** La donnée lue se cite dans la réponse (combien de lignes, quel
état), et l'environnement lu se nomme. C'est ce qui distingue un diagnostic
d'une seconde hypothèse.

Voir aussi [[verifier-chaque-commit-du-decoupage]],
[[un-rapport-d-agent-est-une-piste-pas-un-fait]],
[[refuser-plutot-que-convertir]].
