---
titre: Un périphérique simulé par les tests ne voit pas l'en-tête qui l'interdit
type: lecon
origine: FIBDA CONNECT — 2026-11-11
tags: [tests, navigateur, securite, recette]
---

# Un périphérique simulé par les tests ne voit pas l'en-tête qui l'interdit

**Symptôme.** Le selfie de l'inscription passait tous les e2e (caméra simulée par Playwright). En ligne, la vraie caméra ne s'ouvrait pas.

**Cause.** L'en-tête de sécurité posait `Permissions-Policy: camera=()` : caméra interdite à tout le site. La fausse caméra des tests court-circuitait le chemin réel ; aucun test ne lisait la politique effectivement servie.

**Règle.** Quand un test simule un périphérique ou une permission (caméra, micro, géolocalisation, presse-papiers), un test séparé vérifie que la page servie l'autorise : en-tête lu par requête, ou `document.featurePolicy.allowsFeature(...)`. Tout durcissement d'en-têtes se relit contre la liste des fonctionnalités qui en ont besoin.

**Corollaire.** La recette sur le site déployé lit les en-têtes servis, pas ceux du code.

Voir aussi : [[regarder-l-application-fait-partie-de-la-recette]], [[un-test-de-route-emprunte-le-chemin-de-l-ecran]], [[une-fonctionnalite-mise-en-scene-est-pire-qu-absente]]
