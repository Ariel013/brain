---
titre: Une clé, un usage ; un texte signé dit à quoi il sert
type: lecon
origine: Kalybris — 2026-10-09 (petit matin)
tags: [securite, cryptographie, signature, rotation]
---

# Une clé, un usage ; un texte signé dit à quoi il sert

**Symptôme.** Le registre des stupéfiants signe chaque ligne en RS256 « avec
la clé privée des jetons, vérifiable par `/auth/jwks` » — commode, pas de
clé à ajouter. La revue montre que la première rotation de la clé des
jetons (geste d'hygiène, ou obligatoire après une fuite) rendrait **toute**
ligne du registre `signature_invalide` dès la première, et les exports déjà
remis à un inspecteur invérifiables. Inversement, l'obligation de garder
un registre opposable interdirait de tourner la clé des jetons. Et la
signature brute d'un JWT du serveur vérifiait comme signature d'un export.

**Cause.** Réutiliser une clé existante a été vu comme une économie ; c'était
coupler deux cycles de vie incompatibles (un jeton vit 15 minutes, un
registre des années) et supprimer toute séparation de domaine entre trois
usages.

**Règle.** **Une clé par usage**, avec son `kid` ; un trousseau de clés
publiques **conservées à vie** pour tout ce qui doit rester vérifiable
après rotation ; et un **préfixe de domaine** dans le texte signé
(`kalybris:registre:v1` + séparateur + corps) pour qu'une signature ne
puisse pas être présentée pour autre chose. La procédure de rotation
s'écrit avec la première clé, pas au premier incident.

Voir [[la-cle-d-administration-ne-va-jamais-cote-client]], [[ecrire-la-decision-avec-le-code]].
