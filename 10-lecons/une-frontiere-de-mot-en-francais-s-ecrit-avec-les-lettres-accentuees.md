---
titre: Une frontière de mot en français s'écrit avec les lettres accentuées, pas avec \b
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [regex, francais, donnees]
---

# Une frontière de mot en français s'écrit avec les lettres accentuées, pas avec `\b`

**Symptôme.** Un dictionnaire rangeait les compétences par catégorie de CV.
« Rédaction de documentation technique » et « Rédaction de spécifications »,
deux compétences réelles en base, tombaient dans « Langages » (le langage R) ;
« Revue de code » dans « Frontend » (Vue) ; « Terraform » dans « Bases de
données » (`orm`).

**Cause.** Sans le drapeau `u`, `\b` ne connaît que `[A-Za-z0-9_]` : « é » est
une frontière, donc `^r\b` reconnaît « Ré… ». Et un terme court sans frontière
du tout (`orm`, `vue`) se trouve au milieu d'autres mots.

**Règle.** En texte français, une frontière de mot s'écrit
`(?<![\p{L}\d])…(?![\p{L}\d])` avec le drapeau `u`. Et un dictionnaire de
correspondance se **mesure sur les vraies données** (ici les 126 compétences
en base) avant d'être dit juste — avec des cas négatifs dans les tests.

Voir [[lire-le-fichier-reel-avant-de-modeliser]], [[mesurer-l-outil-avant-de-conclure]].
