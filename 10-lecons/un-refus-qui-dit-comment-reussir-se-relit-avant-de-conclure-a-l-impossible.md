---
titre: Un refus qui dit comment réussir se relit avant de conclure à l'impossible
type: lecon
origine: outillage Claude Code — 2026-11-20
tags: [methode, outillage, verifier]
---

# Un refus qui dit comment réussir se relit avant de conclure à l'impossible

**Symptôme.** `claude plugin disable bio-research` a échoué. L'agent a conclu
que les plugins synchronisés depuis claude.ai ne se coupaient que depuis
claude.ai, et l'a écrit dans le rapport, la banque de skills et la liste
« à toi ». Deux tours plus tard, `claude plugin disable bio-research@synced` a
fonctionné du premier coup.

**Cause.** Le message d'erreur donnait la solution : « Use plugin@marketplace
format ». Il a été lu comme une impossibilité, pas comme une consigne. La
conclusion fausse s'est ensuite propagée dans trois documents et a renvoyé
l'utilisateur vers une console à laquelle il n'avait pas accès.

**Règle.** Avant d'écrire « impossible » ou « à faire ailleurs », **relire le
message d'erreur en entier et essayer ce qu'il suggère**. Un refus qui nomme un
format, une option ou une commande n'est pas un mur, c'est un mode d'emploi.

**Corollaire.** Une impossibilité affirmée est une affirmation comme une autre :
elle se mesure avant d'entrer dans un rapport
→ [[mesurer-l-outil-avant-de-conclure]].

Voir aussi [[lire-la-donnee-avant-l-hypothese]].
