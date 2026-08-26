---
titre: Ne jamais stager en masse
type: lecon
origine: Synoé — 2026-08-23
tags: [git, securite]
---

# Ne jamais stager en masse

**Symptôme.** `git add -A docs/` a committé un classeur de dossiers médicaux et
une capture portant de vrais noms — **les deux fichiers que l'agent venait
d'écrire qu'il ne fallait pas committer sans confirmation**.

**Cause.** La commande ne regarde pas ce qu'elle ramasse, et l'intention de
l'auteur ne la retient pas.

**Règle.** **Stager les fichiers nommément** : `git add <chemin> <chemin>`.
Jamais `git add -A <dossier>`, jamais `git add .`, dès qu'un fichier non suivi
traîne dans l'arbre. Et lire `git status --short` **avant** de committer, pas
après : la ligne `A` d'un fichier inattendu s'y voit.

**Corollaire.** Un `git status` qui affiche des `??` sensibles est **un signal,
pas un décor**. Tant qu'ils sont là, aucune commande large.

Voir aussi [[workflow-git]], [[travailler-avec-les-agents]].
