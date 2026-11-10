---
titre: Une étape de recette nommée n'est pas une étape lancée
type: lecon
origine: Synoé — 2026-09-08
tags: [recette, tests, agents, outillage]
---

# Une étape de recette nommée n'est pas une étape lancée

**Symptôme.** Un lot de seize corrections, déclaré recetté « typecheck, 743
tests, les deux builds », **ne compilait pas** : sept erreurs de types, dont
trois symboles appelés sans être importés. Le rapport, le journal et le message
de commit portaient tous le mot « typecheck ».

**Cause.** Deux couches, et la seconde est la vraie.

D'abord, la commande n'avait pas été lancée : la ligne de recette avait été
recopiée d'un lot précédent. Mais surtout, **rien n'aurait pu la remplacer** —
les deux scripts de build du dépôt s'écrivent `tsc -b --noCheck && vite build`.
Ils invoquent le vérificateur de types **en lui demandant de ne pas vérifier les
types** : le drapeau ne sert qu'à produire les fichiers de déclaration plus vite.
Un build vert ne dit donc rien sur le typage, et les tests ne chargeaient aucun
écran. Il n'existait, dans toute la recette, **aucune étape capable de voir ces
erreurs**.

**Règle.** Une étape de recette se prouve par **son propre code de sortie**, pas
par une étape voisine qui semble l'englober. Avant d'écrire le nom d'un contrôle
dans un rapport, un journal ou un message de commit : le lancer nommément et
lire ce qu'il renvoie.

Et une fois par projet, **lire ce que les scripts de recette font vraiment** —
un drapeau y désarme régulièrement le contrôle que le nom du script promet :
`--noCheck`, `--no-verify`, `--passWithNoTests`, `|| true`, `continue-on-error`
en intégration continue. Le nom d'un script n'est pas son contenu.

**Corollaire.** C'est la même règle que « ne jamais affirmer un résultat non
mesuré », prise par l'autre bout : ici l'affirmation était de bonne foi, et
l'outil censé la fonder ne la fondait pas.

**Seconde occurrence (FIBDA CONNECT, 2026-11-10).** Contrôle des données sensibles avant commit : `git diff --cached | grep -c …` suivi de `git commit` dans la même commande, séparés par un retour à la ligne. Le contrôle a compté 4 occurrences, et le commit est parti quand même : rien ne reliait le résultat au geste. Les 4 étaient des exemples fictifs de format de téléphone, vérifiés après coup. C'est la famille du `|| true` : un contrôle dont le résultat n'arrête rien n'est qu'un affichage. **Un contrôle qui protège un geste s'enchaîne avec `&&` et un code de sortie, ou se lance seul, avec lecture du résultat avant le geste.**

Voir aussi [[regarder-l-application-fait-partie-de-la-recette]],
[[verifier-chaque-commit-du-decoupage]], [[mesurer-l-outil-avant-de-conclure]],
[[recette-avant-release]].
