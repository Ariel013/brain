---
titre: Une conclusion consignée devient une consigne
type: lecon
origine: Synoé — 2026-08-24
tags: [methode, agents, documentation]
---

# Une conclusion consignée devient une consigne

**Symptôme.** Un diagnostic faux écrit dans `JOURNAL.md` a orienté le travail de
la session suivante vers un défaut inexistant.

**Cause.** Le journal est lu **en premier** par chaque nouvelle instance : c'est
sa raison d'être. Ce qui y est écrit n'est pas une note, c'est une instruction.

**Règle.** **Corriger le document fait partie de la correction du défaut.** Une
conclusion invalidée se retire ou se rature explicitement dans la même session —
pas dans une passe de nettoyage ultérieure, qui n'arrivera pas.

**Conséquence sur l'écriture.** Dans un journal, distinguer par la formulation ce
qui est **vérifié** de ce qui est **supposé**. « Le bundle servi est identique au
build de `main`, vérifié par SHA » et « le déploiement a l'air passé » ne sont
pas la même phrase.

Voir aussi [[continuite-entre-sessions]], [[mesurer-l-outil-avant-de-conclure]].
