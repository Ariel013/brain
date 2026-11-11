---
titre: La CSP du premier chargement vaut pour toute la navigation côté client
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [securite, csp, navigateur, spa]
---

# La CSP du premier chargement vaut pour toute la navigation côté client

**Symptôme.** Ouvrir Cloudflare (script et cadre Turnstile) dans la CSP des seules pages qui portent le widget : la page de connexion chargée directement marche, la même page atteinte par un lien depuis l'accueil se voit refuser le script.

**Cause.** Dans une application à navigation côté client (Next.js, toute SPA), changer de page ne recharge pas le document : la CSP reste celle de la **première** page chargée.

**Règle.** Une source autorisée pour une page atteignable par lien interne s'autorise sur tout le document, ou la page s'atteint par chargement complet. Un test e2e emprunte le chemin réel : arriver ailleurs, puis naviguer par le lien.

Voir aussi : [[un-test-de-route-emprunte-le-chemin-de-l-ecran]], [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]]
