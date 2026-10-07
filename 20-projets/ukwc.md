---
titre: UKWC — United Kizdom World Congress
type: projet
domaine: billetterie et site d'un festival de danse (Bénin), projet client
statut: repris le 2026-10-07, édition 2026 terminée, mode « coming soon » 2027
depot: ~/PROJETS/ukwc (pilotage) · ukwc-frontend/ · ukwc-backend/
maj: 2026-10-07
---

# UKWC — United Kizdom World Congress

**Ce que c'est.** Site et billetterie du festival de kizomba United Kizdom
World Congress (Cotonou, Bénin), développé par Kevin pour un client, avec un
collègue (Ariel013) qui a poussé sur une branche `master` en juillet 2026.
Édition 2026 passée ; le site tourne en « coming soon » pour l'édition 2027
(13–18 juillet 2027). Repris le 2026-10-07 avec un audit complet.

**Stack.** Nuxt 4 en statique (LWS mutualisé) + Laravel 13 / MySQL (sous-
domaine API chez LWS). FedaPay pour le Mobile Money, Resend, Cloudinary.
Admin par token Sanctum, scanner QR, points de vente physiques. Zéro test
backend à la reprise.

**La contrainte qui commande le reste.** Deux dépôts de code livrés au client
avec leur propre CD ; la méthode vit dans un dépôt de pilotage au-dessus
(ADR 0001). Données clients réelles en base de prod : rien n'en entre dans
les dépôts.

## Ce que ce projet a appris au coffre

*(À remplir au fil des sessions.)*

- Deux leçons locales candidates, pas encore montées : un `sed` global
  réécrit ses propres commentaires explicatifs ; un Chrome headless à 390 px
  n'est pas un mobile (largeur minimale de fenêtre).

## Ce qui vaudrait d'être repris ailleurs

- **Dépôt de pilotage au-dessus de dépôts clients** : méthode personnelle
  versionnée sans la pousser chez le client, `CLAUDE.md` lu par remontée
  d'arborescence.
- **Mise en sourdine d'un site saisonnier** : commenter + rediriger à deux
  niveaux (règles statiques et middleware client), avec un ADR qui dit comment
  rouvrir.
- **Audit de reprise** comme premier livrable, avant tout code.
