---
titre: Refaire depuis une copie figée ne reprend pas la source — et « vérifié » ne dit pas que l'ajout y est
type: lecon
origine: Optimisation CV — 2026-11-01 et 2026-11-12
tags: [donnees, regeneration, verification]
---

# Refaire depuis une copie figée ne reprend pas la source — et « vérifié » ne dit pas que l'ajout y est

**Symptôme.** Une puce ajoutée au CV de base (`contenu.json`) devait entrer
dans les 71 CV deux colonnes des candidatures en cours. Le script de
régénération les a tous refaits : « 71 vérifiés », une page chacun. Aucun ne
portait la puce. Seul un comptage de la phrase dans le texte extrait l'a
montré (0 sur 154 copies portaient le champ).

**Cause.** Chaque candidature garde une **copie figée** du CV pris au moment
de l'adaptation. Le script rendait cette copie : refaire, c'était relire
l'ancien état. Et la vérification contrôlait la forme (une page, accents,
textes attendus de la copie), pas la présence du changement visé — elle
passait donc aussi bien sans lui.

**Règle.** Avant de « refaire » des sorties pour propager un changement,
savoir d'où le générateur lit : la source vivante ou un instantané. Ce qui
n'appartient pas à l'instantané (mise en forme, ajouts propres à un format,
données de référence) se relit dans la source au moment de refaire. Puis
**vérifier le changement lui-même** dans la sortie (le chercher, le compter),
pas seulement que la sortie passe ses contrôles habituels.

**Corollaire.** Une correction de fait dans la source ne corrige pas non plus
les copies déjà faites (même projet, 2026-10-27 : 13 CV adaptés gardaient
l'ancienne stack) : chercher le terme corrigé dans les copies et les refaire.

**Dans l'autre sens (même projet, 2026-11-12).** Une copie faite **en aval**
ne suit pas davantage : le CV validé avait été recopié dans un dossier
« à envoyer » au moment de la validation ; le CV refait avec le nouveau
contact n'y est jamais arrivé, et l'utilisateur allait envoyer l'ancien. Toute
régénération refait aussi les copies qu'on en a tirées — sauf celles déjà
parties, qui gardent ce qui a été envoyé.

Voir [[une-sortie-verifiee-ne-se-remplace-que-par-une-sortie-verifiee]], [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]], [[un-lot-qui-ecrit-sur-les-vraies-donnees-s-essaie-sur-un-seul-element]], [[mesurer-l-outil-avant-de-conclure]].
