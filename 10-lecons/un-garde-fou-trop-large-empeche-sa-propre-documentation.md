---
titre: Un garde-fou trop large empêche sa propre documentation
type: lecon
origine: Kalybris — 2026-09-05
tags: [outillage, garde-fou, agents]
---

# Un garde-fou trop large empêche sa propre documentation

**Symptôme.** Un hook interdisait à l'agent d'envoyer du code sur la remote.
Écrire le fichier `README.md` qui **documentait ce hook** a été refusé : le
texte citait la commande interdite une dizaine de fois. Puis écrire le
**correctif du hook** a été refusé aussi, pour exactement la même raison. Deux
fois la même erreur en dix minutes, et la seconde fois sur le geste censé
réparer la première.

**Cause.** Le garde-fou confondait ce qui va **s'exécuter** et ce qui va
**s'écrire**. Le corps d'un document en ligne (`cat > fichier <<FIN`) est une
donnée déposée sur disque, pas une commande. La détection cherchait la chaîne
partout dans l'entrée, sans distinguer les deux.

**Règle.** Un garde-fou syntaxique doit décider **sur ce qui sera exécuté**, pas
sur le texte brut de la commande. Concrètement, pour un filtre de shell : on
retire de l'analyse le corps des documents en ligne redirigés vers un fichier,
et on garde l'analyse pour ceux qui sont passés à un interpréteur — c'est la
seule distinction qui rende le filtre à la fois sûr et utilisable.

**Ce que ça coûte de se tromper de côté.** Un faux négatif laisse passer
l'action interdite. Un faux positif, lui, **bloque le travail qui documente le
garde-fou et celui qui le corrige** — il se retourne contre sa propre
maintenance. Le déséquilibre reste bon (mieux vaut bloquer trop que trop peu)
mais il a une borne : un filtre qui empêche d'écrire sur son propre sujet est
passé de l'autre côté.

**Corollaire de méthode, plus important que la règle.** Les deux faux positifs
sont devenus des **cas de recette avant** que le hook ne soit corrigé. Un
garde-fou s'écrit avec sa recette du premier jet, et cette recette contient
autant de « doit passer » que de « doit bloquer » — les deux premiers défauts
du hook (saut de ligne traité comme un espace, entrée illisible non couverte)
ont été trouvés par le test, pas en usage.

**Et la conséquence pratique à connaître.** Les fichiers qui citent la commande
interdite ne peuvent plus être écrits depuis un document en ligne passé à un
interpréteur. Ils s'éditent avec un outil d'écriture de fichier. Ce n'est pas un
contournement : c'est la conséquence normale d'un garde-fou qui fait son
travail.

Voir aussi [[casser-le-test-expres]], [[un-garde-fou-local-se-leve-hors-ligne]].
