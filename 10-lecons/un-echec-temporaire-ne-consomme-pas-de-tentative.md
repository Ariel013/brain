---
titre: Un échec temporaire ne consomme pas de tentative
type: lecon
origine: Kalybris — 2026-10-08 (nuit)
tags: [hors-ligne, synchronisation, file, resilience]
---

# Un échec temporaire ne consomme pas de tentative

**Symptôme.** La file de synchronisation du poste avait une borne unique :
huit tentatives, puis l'opération passe « abandonnée » et bloque la file.
Écrite au sprint des fondations, testée, verte. Le sprint suivant y fait
passer des **ventes encaissées** : une nuit hors ligne (la boucle passe
toutes les 60 s), et la première vente de la file est abandonnée ; la
seule action offerte à l'écran est « neutraliser ». La vente n'atteint
jamais le serveur — ni journal, ni stock, ni ardoise.

**Cause.** La borne protégeait contre une opération *définitivement*
mauvaise qu'on rejouerait sans fin. Elle comptait de la même façon
« réseau injoignable », « jeton expiré » et « 422 » — alors que les deux
premiers ne disent rien de l'opération.

**Règle.** Classer chaque échec par **nature** avant de compter : réseau ou
session → aucune borne, recul seulement ; serveur (5xx/429) → borne puis
retour en attente, jamais d'abandon ; refus de droit → borne courte puis
abandon ; refus métier (4xx à code) → rejet immédiat, sans bloquer la file.
Et une opération abandonnée se **remet en file** par un humain, pas
seulement se neutralise.

**Corollaire.** Un mécanisme écrit « pour plus tard » se relit quand le
« plus tard » arrive : ce qui était acceptable pour un écho de test ne
l'est plus pour une vente.

Voir [[un-garde-fou-local-se-leve-hors-ligne]], [[un-verrou-se-livre-avec-sa-voie-de-correction]].
