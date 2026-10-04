---
titre: Retirer une règle devant un repli fait tomber le cas dans le repli
type: lecon
origine: Synoé — 2026-10-04
tags: [donnees, import, classement]
---

# Retirer une règle devant un repli fait tomber le cas dans le repli

**Symptôme.** Une colonne de fichier (« SpO2 ») ne devait plus être importée :
la donnée n'était plus saisie ni affichée nulle part. La règle qui la
reconnaissait a été retirée de la table de correspondance. Typecheck vert, tests
verts — et la colonne aurait continué d'entrer au dossier et de s'afficher, sous
son en-tête d'origine. Relevé en relecture, avant livraison.

**Cause.** Le classeur d'en-têtes a un **repli** : une colonne qu'il ne reconnaît
pas n'est pas jetée, elle est reprise comme « colonne libre » — choix délibéré,
pour ne pas appauvrir le fichier d'un cabinet. Retirer une règle ne supprime
donc pas le cas : il le **déplace** vers le repli, qui l'accepte. « Ne plus
reconnaître » et « refuser » ne sont pas le même geste dès qu'il existe un
attrape-tout derrière.

**Règle.** Devant tout classement qui se termine par un repli (colonne libre,
`default`, route générique, catégorie « autre »), **on n'exclut pas un cas en
retirant sa règle : on ajoute une règle qui l'écarte**, placée avant le repli —
et un test qui prouve qu'il n'y tombe pas.

**Corollaire.** Avant de retirer une branche, lire ce qui se passe quand **aucune**
branche ne répond. C'est ce chemin-là que le cas va prendre.

Voir aussi [[une-enumeration-de-champs-se-teste]], [[le-calcul-sort-de-l-ecran]],
[[ce-que-l-ecran-promet-le-code-le-fait]], [[un-rapport-d-agent-est-une-piste-pas-un-fait]].
