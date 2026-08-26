---
titre: Ce que l'écran promet, le code doit le faire
type: lecon
origine: Synoé — 2026-08-22
tags: [front, revue]
---

# Ce que l'écran promet, le code doit le faire

**Symptôme.** Trois défauts du même chantier partageaient une forme : l'interface
affirmait une chose, le code en faisait une autre, et **rien ne le signalait**.
Un total de lignes affiché alors que cinq seulement étaient lues. Un nom de
fichier affiché alors que le jeu de démonstration était chargé. Un rapprochement
affiché, puis recalculé autrement à l'enregistrement.

**Cause.** Aucun ne se voit en relisant une fonction : chacune, prise seule, est
correcte. Le défaut est dans **l'écart** entre l'affirmation et le calcul.

**Règle.** Devant tout écran qui affiche un total, un décompte, un état ou un
résultat de calcul, poser une question de plus : **« ce que l'écran promet
est-il ce que le code fait ? »**

**Corollaire.** Un **repli silencieux est un mensonge**. Quand une entrée ne peut
pas être traitée, la refuser **en disant pourquoi**. Charger autre chose à la
place est toujours pire que de ne rien charger.

Voir aussi [[le-calcul-sort-de-l-ecran]], [[refuser-plutot-que-convertir]].
