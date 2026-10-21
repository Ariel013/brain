---
titre: Un lien venu d'une donnée se contrôle sur l'adresse résolue, pas sur son texte
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [securite, ssrf, reseau]
---

# Un lien venu d'une donnée se contrôle sur l'adresse résolue, pas sur son texte

**Symptôme.** Un script relisait les pages d'offres d'emploi (liens venus
d'API ou d'ajouts manuels) pour savoir si elles étaient fermées. Il refusait
`localhost` et `127.…` dans le lien. La relecture de sécurité a fait passer
`http://localhost.:3000/` (point final) et un nom public qui résout vers
127.0.0.1 : l'application locale, sans authentification, écoutait là.

**Cause.** Le contrôle portait sur le **texte** du nom, alors que le danger
est l'**adresse** à laquelle on se connecte — qu'un nom, une redirection ou un
rebinding DNS peuvent changer après le contrôle.

**Règle.** Quand le code ouvre un lien qui vient d'une donnée : résoudre le
nom, refuser toute adresse privée, de bouclage ou réservée (IPv4 et IPv6,
`::ffff:` comprises), **se connecter à l'adresse vérifiée**, et refaire le
contrôle à **chaque** redirection (et refuser https → http). Un filtre de
texte n'est qu'un premier tamis.

Voir [[le-client-n-est-jamais-une-autorite]], [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]].
