---
titre: Un acte porte son auteur ; le droit se juge sur l'auteur, pas sur le transporteur
type: lecon
origine: Kalybris — 2026-10-11
tags: [securite, hors-ligne, synchronisation, droits]
---

# Un acte porte son auteur ; le droit se juge sur l'auteur, pas sur le transporteur

**Symptôme.** File de synchronisation hors ligne, depuis le premier sprint.
Une caissière sans droit d'annuler annule une vente pendant une coupure,
se déconnecte ; le titulaire se connecte, la file part sous **son** jeton :
le serveur accepte, et le journal immuable attribue l'annulation au
titulaire. Huit revues avant celle qui l'a vu.

**Cause.** Une opération en file ne portait que son contenu ; le serveur
jugeait le droit sur la session qui envoyait. En ligne, envoyeur et auteur
sont la même personne ; hors ligne, plus du tout.

**Règle.** Chaque opération mise en file porte l'identité de la session
**au moment de l'acte**, jamais réécrite ; le serveur établit cette
session, juge le droit sur elle à l'heure de l'acte, et garde le
transporteur dans la trace. Corollaire payé dans la foulée : **un
identifiant de session n'est pas un secret** — écrit en clair sur le
poste, il se lit et se réclame. L'auteur se prouve par une signature d'une
clé non extractible de la session, pas par un identifiant.

Voir [[le-client-n-est-jamais-une-autorite]], [[un-echec-temporaire-ne-consomme-pas-de-tentative]].
