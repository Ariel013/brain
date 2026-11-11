---
titre: Une limite de débit anonyme se nomme — throttle:N,M partage son compteur
type: lecon
origine: UKWC — 2026-11-11
tags: [securite, laravel, api]
---

# Une limite de débit anonyme se nomme — `throttle:N,M` partage son compteur

**Symptôme.** Formulaire public d'inscription (Laravel), protégé par
`throttle:10,1` comme les autres routes publiques. La relecture sécurité
signale qu'un pic d'inscriptions après un partage dans un groupe WhatsApp
renverrait des 429. Le formulaire n'affichait alors qu'un « Une erreur est
survenue » générique.

**Cause.** Pour un visiteur non connecté, `ThrottleRequests` clé le compteur
sur `domaine|IP`, **sans la route** (vérifié dans
`ThrottleRequests::resolveRequestSignature`). Toutes les routes en
`throttle:N,M` partagent donc le même compteur par IP : paiement, inscription,
etc. Et sur les réseaux mobiles africains, beaucoup de visiteurs sortent par
la même IP (CGNAT) : le plafond par personne devient un plafond par opérateur.

**Règle.** Chaque formulaire public a son **limiteur nommé**
(`RateLimiter::for('inscription', …)` avec une clé `route|ip`), un plafond par
minute **et** par jour, dimensionné pour une IP partagée. L'écran traite le 429
avec un message propre (« trop de tentatives depuis ce réseau »). L'abus se
borne aussi ailleurs : index unique, champ piège.

Voir [[un-rapport-d-agent-est-une-piste-pas-un-fait]],
[[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]].
