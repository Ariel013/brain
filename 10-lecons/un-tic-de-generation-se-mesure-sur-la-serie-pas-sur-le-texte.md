---
titre: Un tic de génération se mesure sur la série, pas sur le texte — interdire un tic en fait naître un autre
type: lecon
origine: Optimisation CV — 2026-11-03
tags: [ia, generation, verification, qualite-redactionnelle]
---

# Un tic de génération se mesure sur la série, pas sur le texte — interdire un tic en fait naître un autre

**Symptôme.** Pour corriger des lettres de motivation générées par un modèle
qui ouvraient toutes sur les mêmes accroches artificielles, on a ajouté au
moule une exigence de qualité rédactionnelle et un contrôle qui refuse ces
accroches. Chaque lettre de la série refaite passait ses contrôles. Lues en
lot, elles avaient de nouveaux tics : EPITECH cité dans 33 lettres sur 35,
et 10 lettres ouvrant sur « Ce qui m'attire… ».

**Cause.** Deux choses. Le contrôle jugeait **chaque texte seul** — or une
répétition est une propriété de la série, invisible dans une lettre isolée.
Et interdire une tournure ne retire pas au modèle son besoin d'une tournure
sûre : il se rabat sur la suivante, et sur ce que le moule lui propose par
défaut (la phrase EPITECH, facultative en principe, était pré-remplie).

**Règle.** Après toute consigne de style donnée à un modèle, **mesurer la
série entière** avant de la livrer : compter les ouvertures, les noms et les
formules récurrentes sur l'ensemble, pas seulement relire un échantillon. Un
élément facultatif du moule est **vide par défaut**, sinon il devient
systématique. La correction s'est mesurée : sur la seconde série, EPITECH
dans 22 lettres sur 35, aucune ouverture répétée plus de deux fois.

**Corollaire.** Une liste de tournures interdites ne converge pas seule :
chaque refus déplace le tic. Elle se double d'une mesure de répartition sur
le lot, refaite à chaque nouvelle série.

Voir [[mesurer-l-outil-avant-de-conclure]], [[refaire-depuis-une-copie-figee-ne-reprend-pas-la-source]], [[une-proposition-s-affiche-elle-ne-se-preselectionne-pas]].
