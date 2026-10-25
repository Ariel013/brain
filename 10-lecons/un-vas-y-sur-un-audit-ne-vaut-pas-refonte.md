---
titre: Un « vas-y » sur une liste de recommandations ne vaut pas mandat de refonte
type: lecon
origine: Portfolio — 2026-10-25
tags: [front, design, agents, perimetre]
---

# Un « vas-y » sur une liste de recommandations ne vaut pas mandat de refonte

**Symptôme.** Un audit `impeccable` du portfolio rend 9/20 et une liste
d'actions : durcir, recolorer, épurer, optimiser, adapter. Réponse : « vas-y ».
L'agent enchaîne tout : nouvelle palette, nouvelle police, sections réécrites
façon CV, carrousels et modales supprimés, deux dépendances retirées. Le build
passe, les contrastes sont mesurés, le rendu est vérifié aux trois largeurs. Le
retour : « non annule […] il s'éloigne de ce que j'avais […] je préfère mon
ancien portfolio ». Tout est jeté ; seules les petites corrections invisibles
sont refaites.

**Cause.** L'audit mélangeait deux natures de travail : des **corrections**
(faux identifiant affiché, textes non traduits, modales sans Échap, contraste)
et un **changement d'identité** (le jugement « ça fait IA » porté par la
skill). « Vas-y » a été lu comme un accord sur les deux. Or une refonte
visuelle est un choix **structurant** : elle aurait dû s'arrêter et se poser,
comme le dit déjà [[concevoir-le-front]] (« une charte existante se reprend et
s'améliore, elle ne se jette pas »). L'interview de `teach` a même montré la
préférence, « trucs simples et légers », mais sur un site existant elle
décrivait un réglage, pas une table rase.

**Règle.** Sur une interface qui existe déjà, séparer les recommandations en
deux lots avant d'agir :
1. **ce qui ne change pas l'apparence** (données fausses, traductions,
   accessibilité au clavier et lecteurs d'écran, performance invisible) :
   s'applique sur un « vas-y » ;
2. **ce qui change ce qu'on voit** (couleurs, typographie, mise en page,
   composants retirés) : se propose **élément par élément**, avec l'écart
   visible annoncé, et attend un accord explicite pour chacun.

**Corollaire.** Le verdict esthétique d'un outil (« AI slop ») n'est pas celui
du propriétaire. Il se rapporte comme un avis, jamais comme un défaut à
corriger d'office. Et quand un changement visible est accepté, annoncer son
ampleur réelle : ici, un « à peine visible » promis s'est révélé nettement
visible une fois la norme de contraste appliquée.

Voir [[concevoir-le-front]], [[ce-que-l-ecran-promet-le-code-le-fait]],
[[regarder-l-application-fait-partie-de-la-recette]].
