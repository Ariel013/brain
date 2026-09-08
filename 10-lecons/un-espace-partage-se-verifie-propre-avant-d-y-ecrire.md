---
titre: Un espace partagé se vérifie propre avant qu'on y écrive
type: lecon
origine: brain — 2026-09-08 (déclenché par une session Synoé)
tags: [git, methode, agents, coffre]
---

# Un espace partagé se vérifie propre avant qu'on y écrive

**Symptôme.** Au moment de committer deux notes dans le coffre de méthode, `git
status` a montré **cinq fichiers indexés qui n'étaient pas les miens** : deux
leçons et une fiche de projet, écrites deux jours plus tôt par une session d'un
**autre projet**. Un commit sans vérification les emportait toutes, mêlant deux
projets sans rapport dans un même lot — et donnant à l'utilisateur l'impression
qu'un projet étranger s'était glissé chez lui.

**Cause.** Deux erreurs qui se sont additionnées.

La session précédente avait fait `git add` **en attendant** une validation qui
n'est jamais venue, et s'est terminée en laissant l'index sale. Rien ne le
signalait à la suivante.

Et le dépôt partagé porte un **index commun** — ici `10-lecons/lecons.md`, où
chaque projet ajoute ses lignes. Le fichier apparaît alors en `MM` : une partie
indexée par l'autre session, une partie modifiée par la mienne. Committer « mes »
fichiers y emportait ses lignes **sans les notes qu'elles citent** — un index
pointant vers des fichiers absents.

**Règle.** Dans tout espace écrit par plusieurs sessions ou plusieurs projets —
coffre de méthode, dépôt de documentation, monorepo — **`git status` d'abord,
avant d'écrire une ligne**. Ce qui traîne et qui n'est pas de toi ne s'absorbe
pas, ne se supprime pas : il se **signale**, et se committe **à part et en
premier** si l'utilisateur le valide.

**Corollaire, et c'est lui qui ferme la boucle : ne jamais `git add` en
attendant une validation.** Un fichier indexé « pour être prêt » est un fichier
qu'on abandonne dans l'index quand la conversation tourne. Laisser les
modifications non indexées, et stager **nommément** au moment de committer —
jamais avant.

Voir aussi [[stager-nommement]], [[nommer-la-copie-visee]],
[[une-conclusion-consignee-devient-consigne]].
