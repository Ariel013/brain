---
titre: Un acte passé se juge sur des faits datés, jamais sur un état courant
type: lecon
origine: Kalybris — 2026-10-09 (petit matin)
tags: [hors-ligne, synchronisation, securite, sessions]
---

# Un acte passé se juge sur des faits datés, jamais sur un état courant

**Symptôme.** Une vente sous ordonnance, validée hors ligne par un
pharmacien dont la session était vivante, remonte au serveur le
surlendemain. Entre-temps la maintenance quotidienne a purgé les sessions
expirées, et un inconnu a verrouillé le compte du pharmacien avec cinq
codes faux. Le serveur refuse la vente **définitivement** (403) : elle a
eu lieu, l'ordonnancier ne la recevra jamais. Reproduit par la revue de
sécurité, pas par les tests — qui synchronisaient tous dans la seconde.

**Cause.** La vérification lisait l'état **présent** (`actif`,
`verrouille`, existence de la session) pour juger un acte daté d'avant.
Dans un système hors ligne, « maintenant » et « au moment de l'acte » sont
deux instants, et seul le second compte.

**Règle.** Toute vérification d'un acte remonté compare des **faits datés**
à la date de l'acte : session émise avant, expirée après, révoquée après,
compte désactivé après. Les faits nécessaires se **conservent au moins la
fenêtre du hors-ligne** (ici 45 jours après expiration) — une purge trop
tôt est une perte de preuve. Et un refus dû à un état transitoire n'est
jamais définitif.

**Corollaire.** Un registre légal date l'**acte**, pas son enregistrement :
`dispensee_at` (horloge du poste, bornée) à côté de `created_at` serveur.

Voir [[un-garde-fou-local-se-leve-hors-ligne]], [[refuser-plutot-que-convertir]].
