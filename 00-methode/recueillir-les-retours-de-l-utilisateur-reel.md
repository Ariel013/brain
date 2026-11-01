---
titre: Recueillir les retours de l'utilisateur réel
aliases: [Utilisateur réel, Guide d'entretien, Retours utilisateur]
type: methode
origine: Synoé, prompt d'amorce d'origine (2026-08-23), parties 3.7 et 5
maj: 2026-11-01
---

# Recueillir les retours de l'utilisateur réel

> **Un utilisateur réel est le moteur du produit.** Tant qu'il n'a pas touché
> l'outil, tout ce qu'on construit repose sur des suppositions. L'écrire
> explicitement dans le `JOURNAL.md` évite de confondre avancement et progrès.

## Ce qu'on lui remet

- **Un point d'avancement écrit pour le métier** après chaque module, qui nomme
  sans détour ce qui était cassé → [[modele-point-avancement]].
- **Des marches à suivre** qu'il déroule seul, chaque étape fabriquant son
  propre état de départ → [[documents-du-projet]].

## Ce qu'on lui demande d'abord : ses données

**Exiger le fichier réel avant d'écrire le modèle.** Pas une description, pas
une capture : le fichier. S'il ne peut pas le fournir, c'est le premier point
bloquant du projet, à traiter comme tel → [[lire-le-fichier-reel-avant-de-modeliser]].

## Le guide d'entretien

Les cinq règles qui ont le mieux marché pour récolter ses retours :

1. **Demander ce qu'il a fait**, pas ce qu'il pense.
2. **Ne jamais défendre l'outil.** La seule bonne réponse à une critique est
   « raconte-moi ».
3. **Laisser le silence** trois secondes : le vrai reproche vient après la
   formule polie.
4. **Noter ses mots exacts**, surtout le vocabulaire métier. S'il dit « fiche »
   là où l'application dit « dossier », c'est l'application qui a tort
   → [[conventions-de-code]].
5. **Ne pas lui demander de concevoir.** Chercher le problème ; la solution est
   notre travail.

**Aucune donnée réelle** dans les notes d'entretien, les captures ou les
maquettes.

## Les questions en attente

Sur Synoé, plusieurs questions à l'utilisatrice ont traîné dans `A-FAIRE.md`
sans jamais être posées, et ont bloqué l'ouverture de chantiers entiers.

- Les questions sont tenues dans la table « Décisions en attente » de
  `A-FAIRE.md` ([[modele-a-faire-md]]) et **posées en lot à chaque point
  d'avancement**, jamais transformées en blocage de la tâche en cours.
- Une question qui traîne **plus de deux sessions** est soit tranchée par
  défaut avec l'hypothèse écrite, soit déclarée bloquante. Elle ne dort pas.

Voir aussi [[amorce-nouveau-projet]].
