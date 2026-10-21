---
titre: Une action irréversible a trois issues — faite, pas faite, incertaine — et l'incertaine bloque la répétition
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [resilience, envoi, idempotence, verification]
---

# Une action irréversible a trois issues — faite, pas faite, incertaine — et l'incertaine bloque la répétition

**Symptôme.** Un envoi d'e-mail de candidature affichait « Rien n'est parti »
dès que l'appel levait une erreur, et rouvrait le formulaire. Les relectures
ont trouvé deux cas où c'était faux : une coupure réseau **après** que le
serveur SMTP a accepté le message, et une erreur d'écriture en base **après**
un envoi réussi (le `try` couvrait l'envoi et les écritures). Kevin aurait
renvoyé : le recruteur recevait deux fois le même e-mail.

**Cause.** Le code traitait l'issue comme binaire. Pour une action qui sort du
système (e-mail, paiement, appel d'API avec effet), une erreur ne prouve pas
que rien ne s'est passé : elle prouve seulement qu'on ne sait pas.

**Règle.**
1. Classer l'erreur : **refus sûr** (connexion, authentification, destinataire
   refusés, code de réponse explicite) → « pas faite » ; tout le reste
   (délai, coupure pendant ou après la remise) → **incertaine**.
2. L'incertaine **bloque toute répétition** de l'action jusqu'à ce qu'un humain
   tranche (« il est dans mes Envoyés » / « il n'y est pas »).
3. Seul l'appel externe va dans le `try` ; une erreur d'écriture **après** un
   succès se dit « fait, enregistrement à vérifier », jamais « pas fait ».
4. La réservation de l'action (brouillon → en cours) est atomique : un double
   clic n'en produit qu'une.

**Corollaire.** « Rien n'est parti » est une affirmation : elle se mesure comme
une autre ([[mesurer-l-outil-avant-de-conclure]]).

Voir [[un-echec-temporaire-ne-consomme-pas-de-tentative]], [[ce-que-l-ecran-promet-le-code-le-fait]].
