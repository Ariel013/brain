---
titre: Une consigne exécutable se rédige contre le code, pas contre le journal
type: lecon
origine: Synoé — 2026-09-08
tags: [documentation, utilisateur, agents]
---

# Une consigne exécutable se rédige contre le code, pas contre le journal

**Symptôme.** Une marche à suivre écrite pour l'utilisatrice — vingt-quatre
gestes à dérouler pour vérifier autant de corrections — portait deux consignes
fausses. Elle lui demandait de constater qu'un import « n'enregistre plus » des
valeurs aberrantes, alors que l'écran **refuse l'injection entière** et la
ramène sur la première ligne fautive ; et elle la renvoyait vers le mauvais
compteur, « Incohérences » là où l'écran affiche « Valeurs refusées ».

**Cause.** L'attendu avait été repris du `JOURNAL.md`, qui disait vrai — « refuse
d'injecter les valeurs qu'il affiche en rouge » — mais qui résume **l'intention**
d'une correction. Une consigne à exécuter a besoin du **comportement**, au geste
et au libellé près. Entre les deux il n'y a pas d'erreur, il y a un changement de
nature que rien ne signale.

**Règle.** Toute consigne qu'un humain va **exécuter** — marche à suivre, recette,
procédure d'exploitation, libellé d'erreur cité dans un document — se relit
**dans le code de l'écran concerné** avant d'être écrite. Le journal et les ADR
disent pourquoi ; ils ne disent pas ce qui s'affiche.

**Corollaire, et c'est lui qui coûte cher.** Une consigne fausse ne produit pas
une hésitation, elle produit un **faux négatif** : l'utilisateur fait le geste,
n'obtient pas ce qui est annoncé, et conclut que la correction a échoué. On
rouvre alors un défaut qui n'existe pas — et, la fois suivante, on le croit
moins quand il existe.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]],
[[une-conclusion-consignee-devient-consigne]],
[[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]].
