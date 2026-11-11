---
titre: Un en-tête ajouté par les tests part aussi vers les services tiers
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [tests, playwright, integration]
---

# Un en-tête ajouté par les tests part aussi vers les services tiers

**Symptôme.** Avec les clés de test Cloudflare, le vrai widget Turnstile échouait dans les e2e alors qu'il marchait à la main.

**Cause.** `page.setExtraHTTPHeaders({ 'cf-connecting-ip' })`, posé pour simuler Cloudflare devant notre site (une IP par test pour les limites de l'API), vaut pour **toutes** les requêtes de la page : il partait aussi vers `challenges.cloudflare.com`, qui refuse cet en-tête venant d'un client.

**Règle.** Un en-tête de test destiné à son propre serveur se pose par `page.route` limité à son origine, jamais pour toute la page. Dès qu'une suite parle à un service tiers réel, lister ce que le navigateur de test ajoute à chaque requête.

Voir aussi : [[mesurer-l-outil-avant-de-conclure]], [[un-test-se-borne-a-son-propre-jeu-de-donnees]]
