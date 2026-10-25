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

**Seconde occurrence — Portfolio, 2026-10-25.** La carte des certifications
affichait un « ID DE VALIDATION » obtenu en prenant le dernier segment de
l'URL du certificat. Pour les examens blancs, ce segment était le nom du
fichier image (`…_CAP-MOCK-EXAM_bugaco.jpg`) : l'écran présentait comme
identifiant vérifiable ce qui n'en était pas un, juste après un commit qui
corrigeait la présentation de ces mêmes examens. Correction : champ retiré,
faute d'un vrai identifiant dans les données. Une étiquette qui affirme une
nature (« ID », « vérifié », « date d'émission ») exige une donnée de cette
nature, pas une valeur devinée.

Voir aussi [[le-calcul-sort-de-l-ecran]], [[refuser-plutot-que-convertir]].
