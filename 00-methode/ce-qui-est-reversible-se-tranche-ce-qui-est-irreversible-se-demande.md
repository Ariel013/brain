---
titre: Ce qui est réversible se tranche, ce qui est irréversible se demande
aliases: [Autonomie, Conditions d'arrêt, Faire tourner l'agent en autonomie]
type: methode
origine: Synoé, prompt d'amorce d'origine (2026-08-23), parties 1 et 6
maj: 2026-11-01
---

# Ce qui est réversible se tranche, ce qui est irréversible se demande

> L'autonomie ne s'obtient pas en disant « fais ce que tu veux ». Elle s'obtient
> en posant **trois choses par écrit** : une file de tâches ordonnée avec des
> critères d'acceptation, une barrière de vérification que l'agent franchit
> seul, et une liste explicite de ce qui l'oblige à s'arrêter. Tout le reste, il
> le fait sans moi et me le raconte à la fin dans le [[rapport-de-tache]].

## Le principe d'arbitrage

Un mauvais nom de fonction se renomme ; un `git push` ne se dé-pousse pas.
**Ce qui est réversible se tranche, ce qui est irréversible se demande.** C'est
la grille qui départage tous les cas que la table ci-dessous ne prévoit pas.

## Les conditions d'arrêt

L'agent va vite tant qu'il sait **exactement** quand il n'a pas le droit
d'avancer. Cette table va dans le `CLAUDE.md` du projet dès le jour 1
([[modele-claude-md]]), courte et sans ambiguïté :

| Il s'arrête et demande | Il tranche seul et documente |
|---|---|
| `git push` (à **chaque** fois, jamais d'accord acquis) | Nom de fichier, nom de fonction, découpage interne |
| Nouvelle dépendance externe | Extraction d'un calcul hors d'un composant |
| Changement de schéma de base de données | Ajout d'un test, correction d'un test rouge |
| Nouvelle table, nouveau flux de données | Choix de mise en page dans le style existant |
| Suppression ou écrasement de données réelles | Refactor local sans changement de comportement |
| Choix produit visible par l'utilisateur final | Correction d'un défaut trouvé en chemin |
| Tout ce qui touche des données sensibles ou la sécurité | Mise à jour des docs qu'il vient de rendre fausses |

Ce qui est tranché seul n'est pas caché : la décision apparaît dans le rapport,
où je l'amende si besoin. J'amende le jugement, pas le code, et ce calibrage se
capitalise.

## La file de tâches : le carburant

Format de tâche : [[modele-backlog]]. Deux champs y font tout le travail
d'autonomie :

- **Les critères d'acceptation** permettent à l'agent de savoir qu'il a fini
  **sans me le demander**. Sans eux, il s'arrête au premier doute : c'est là que
  naît le micro-management.
- **Le hors-périmètre** l'empêche de dériver pendant trois heures. Ce qu'il
  trouve en chemin et ne traite pas part au backlog, rien ne se perd.

L'agent **coche la tâche** quand elle est finie et enchaîne sur la suivante. Il
ne redemande pas « et maintenant ? » : la réponse est écrite. D'où la règle
d'amorce : un backlog rempli **assez loin pour qu'une session entière
s'enchaîne sans question** → [[amorce-nouveau-projet]].

## La barrière de vérification

La recette complète (typecheck, tests, build, passe visuelle) est **la
condition d'entrée du rapport**, pas une option : l'agent ne rend pas compte
tant qu'elle n'est pas verte → [[recette-avant-release]].

Corollaire souvent oublié : **il n'a pas à demander la permission de corriger
ce qu'elle signale.** C'est du travail, pas une décision.

## Enchaîner plusieurs tâches

La formulation qui a marché, à donner en début de session :

> Prends les tâches N à M du backlog, dans l'ordre. Pour chacune : branche
> dédiée, code, recette complète verte, rapport de tâche, commit. **Ne pousse
> rien.** Si tu rencontres une condition d'arrêt, traite les tâches suivantes
> qui n'en dépendent pas et signale-le dans le rapport plutôt que d'attendre.
> Mets `JOURNAL.md` à jour à la fin.

Trois détails changent tout :

- **« Ne pousse rien »** : tant que rien n'est poussé, toute erreur se répare en
  local, **y compris une release ratée**. C'est le filet qui autorise
  l'autonomie.
- **« celles qui n'en dépendent pas »** : sinon un seul blocage met toute la
  session en pause.
- **Un commit par tâche, atomique** : c'est ce qui permet d'amender ou de jeter
  une tâche sans toucher aux autres.

## Réduire les demandes de permission

La plupart des interruptions ne sont pas des décisions : ce sont des
validations de `ls`, `grep`, `git status`. Une liste de permissions pour les
commandes de lecture les supprime, et les confirmations qui restent reprennent
du sens. Détail : [[claude-code]].

Les garde-fous qui dispensent de surveiller (hook `pre-push`, CI, `.gitignore`
défensif, [[stager-nommement]]) sont ce qui rend l'autonomie tenable, pas la
confiance.

## Deux avertissements

- **L'autonomie ne remplace pas le regard.** 480 tests verts, un build vert et
  un typecheck vert coexistaient avec trois écrans qui ne s'affichaient pas
  → [[regarder-l-application-fait-partie-de-la-recette]]. Une passe visuelle
  humaine avant chaque mise en production, même courte.
- **Amender au fil de l'eau, c'est écrire.** Un retour fait en conversation est
  perdu à la session suivante ; devenu une ligne dans `CLAUDE.md`, dans les
  conventions ou dans les leçons, il est acquis. La question après chaque
  correction : **« où est-ce que j'écris ça pour ne jamais avoir à le
  redire ? »** → [[continuite-entre-sessions]]

Voir aussi [[travailler-avec-les-agents]], [[workflow-git]].
