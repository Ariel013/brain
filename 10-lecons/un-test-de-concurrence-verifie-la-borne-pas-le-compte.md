---
titre: Un test de concurrence vérifie la borne, pas un compte exact
type: lecon
origine: FIBDA CONNECT — 2026-11-11
tags: [tests, concurrence, securite]
---

# Un test de concurrence vérifie la borne, pas un compte exact

**Symptôme.** Un test de sécurité vert depuis des jours (« 20 codes 2FA envoyés en même temps : jamais plus de 5 comptés ») échoue une fois, sur une machine chargée : `expected 4 to be 5`. Relancé cinq fois, il repasse.

**Cause.** Le test vérifiait `counted === 5`, alors que la règle est « au plus 5 ». Sous concurrence, un essai déjà compté peut relire sa session après qu'un 6ᵉ essai l'a supprimée : il répond « reconnecte-toi » sans comparer de code. Le serveur était juste ; l'attendu exprimait un ordre d'exécution, pas la propriété.

**Règle.** Un test de course vérifie la propriété de sûreté telle qu'elle s'énonce : une borne (`≤ 5`), un invariant (« une seule réussit », « session supprimée »), et la somme des issues (`401 = 20 − comptés`). Jamais un nombre exact qui dépend de l'entrelacement.

**Corollaire.** Un test fragile sur une garde de sécurité ne se relance pas jusqu'au vert : on lit le chemin qui produit l'autre valeur, et l'on décide si c'est une faille (borne dépassée) ou un attendu trop étroit.

Voir aussi : [[casser-le-test-expres]], [[mesurer-l-outil-avant-de-conclure]], [[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]]
