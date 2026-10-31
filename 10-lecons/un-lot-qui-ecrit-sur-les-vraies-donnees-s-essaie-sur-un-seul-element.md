---
titre: Un lot qui écrit sur les vraies données s'essaie d'abord sur un seul élément
type: lecon
origine: optimisation-cv — 2026-10-31
tags: [donnees, scripts, verification]
---

# Un lot qui écrit sur les vraies données s'essaie d'abord sur un seul élément

**Symptôme.** Un script devait fabriquer, à côté de chaque CV de candidature,
son jumeau en deux colonnes. Lancé d'emblée sur les 53 candidatures en cours,
il répondait « REFUSÉ » ligne après ligne. En allant voir : des fichiers
`ux-colonnes.pdf`, `urt-deux-colonnes.pdf`, `ge-alterne-deux-colonnes.pdf`
dans une dizaine de dossiers de données — 33 fichiers parasites, à retrouver
et supprimer un par un.

**Cause.** Deux défauts qu'un seul essai aurait montrés. Le nom de fichier se
calculait en découpant la chaîne : `cible.slice(resolve(cible, "..").length + 1)`
— la longueur d'un chemin **absolu** appliquée à un chemin **relatif**, d'où
des noms tronqués. Et la vérification exigeait un texte que le second gabarit
réécrivait (« / » devenu « - »), d'où le refus systématique. Les tests
unitaires passaient : ils ne fabriquaient aucun fichier.

**Règle.** Un traitement par lot qui écrit dans les vraies données se lance
d'abord sur **un** élément (un paramètre `max` suffit), puis on regarde ce
qu'il a produit : les noms et emplacements des fichiers, la ligne en base,
l'écran qui la lit. Le lot ne part qu'ensuite. Appliqué le même jour au lot
suivant (19 CV) : un essai, une vérification de bout en bout, puis le reste,
sans incident.

**Corollaire.** Le nom et le dossier d'un chemin s'obtiennent par `basename`
et `dirname`, jamais par découpage de chaîne : le découpage suppose une forme
(absolue, relative, séparateur final) que rien ne garantit.

Voir [[un-test-se-borne-a-son-propre-jeu-de-donnees]],
[[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]],
[[mesurer-l-outil-avant-de-conclure]].
