---
titre: Conventions de code
aliases: [Conventions, Style]
type: methode
maj: 2026-09-17
---

# Conventions de code

Les conventions d'un projet se **déduisent du code déjà écrit** — l'objectif est
la cohérence, pas la ré-invention. En cas de doute : ouvrir un fichier existant
du même type et suivre son style plutôt qu'improviser.

Ce qui suit est ce qui vaut d'un projet à l'autre.

## Langue

- **Le vocabulaire métier est en français**, et ne bascule jamais à mi-projet :
  noms de types, de champs, d'écrans. Un modèle mi-anglais mi-français est un
  modèle qu'on relit deux fois.
- Le vocabulaire technique générique peut rester en anglais si c'est déjà
  l'usage du dépôt.
- Commentaires en français : blocs d'intention en tête de fichier ou de section,
  `//` ciblés pour expliquer **un choix non évident** — pas pour paraphraser la
  ligne suivante.

## Modèle de données

- **Un seul endroit pour les types métier.** Étendre les interfaces existantes
  plutôt que créer des types parallèles.
- **Vocabulaire fermé = `as const` + type dérivé**, jamais des chaînes libres.
- **Famille fermée + libellé libre** plutôt qu'une énumération qui grossit :
  chaque valeur ajoutée à une liste fermée est une modification de code.
  Corollaire : le texte libre ne supprime pas le coût, il le reporte sur la
  lecture. L'assumer, pas le découvrir.
- **Donnée + précision** (`date` + `'exacte' | 'annee'`) plutôt qu'une donnée
  approximative dont on ignore le degré d'approximation. La précision ne fait
  que monter.
- **Un format canonique par donnée**, converti à l'entrée. Deux formats qui
  cohabitent sans conversion explicite finissent par se mélanger
  → [[normaliser-a-la-lecture]].
- **Un champ optionnel est un endroit à auditer**, pas une addition anodine :
  `?` fait taire le compilateur exactement là où on aurait besoin qu'il crie.

## Frontières

- **Isoler la persistance derrière un contrat**, jamais d'appel direct à la base
  depuis un écran → [[isoler-la-persistance-derriere-un-contrat]].
- **Une modification envoie le delta**, jamais l'objet ni l'état entier ; une
  notification s'applique ligne à ligne, sans relecture complète. Le coût réseau
  (taille × fréquence × appareils, contre le quota) se chiffre avant de valider
  → [[une-modification-envoie-ce-qui-a-change-pas-l-etat]].
- **Le calcul ne vit pas dans un composant** : dès qu'un écran calcule, le calcul
  sort dans une lib testable → [[le-calcul-sort-de-l-ecran]].
- **Une action rend l'issue, l'écran rend le message.** La couche métier renvoie
  ce qui s'est passé (`{ ok, erreur }`), l'appelant le traduit. Une même action
  sert alors deux écrans qui n'en disent pas la même chose, et l'issue reste
  testable sans interface.
- **Une ressource distribuée par une couche se libère dans cette couche**, pas
  chez l'appelant — vaut pour toute ressource à cycle de vie (URL, abonnement,
  verrou, fichier ouvert).
- **L'écriture sort de l'action** : ce qui décide de l'état vit dans une
  fonction ordinaire, l'action serveur n'en garde que l'enveloppe (session,
  audit, rafraîchissement) → [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]].
- **Un cache de connexion se pose dans tous les environnements**, jamais
  « seulement en dev » → [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]].

## Interface

- **Un kit de primitives commun**, réutilisé plutôt que des éléments ad hoc.
- **Les jetons de style (couleurs, espacements) au même endroit** — pas de
  valeur en dur dans un composant si un jeton existe.
- **Ce qui doit changer avec la largeur vit dans la feuille de style**, pas dans
  un style en ligne : un style en ligne est hors d'atteinte des requêtes média.
- **Pas de bibliothèque de graphiques** par défaut : CSS/SVG inline. Léger,
  fonctionne hors ligne, et une dépendance de moins à maintenir.
- **Une contrainte technique assumée s'écrit avec sa raison**, comme
  ci-dessus. Sans sa raison, l'instance suivante la prend pour un oubli.

## Données de démonstration

Les jeux de démo vivent dans un fichier dédié et **ne se mélangent jamais** à la
logique de production. Un jeu de démo peut masquer une fonctionnalité absente
pendant des mois → [[verifier-le-chemin-d-ecriture]]. Un test vérifie qu'il
exerce chaque fonctionnalité visible, et il se met à jour dans la même tâche
que le modèle → [[un-jeu-de-demonstration-se-teste-comme-une-fixture]].

## Pièges relevés

- Frontière de mot en français : `(?<![\p{L}\d])…(?![\p{L}\d])` avec le
  drapeau `u`, jamais `\b` seul → [[une-frontiere-de-mot-en-francais-s-ecrit-avec-les-lettres-accentuees]].
- SQL écrit à la main dans un ORM : qualifier la colonne extérieure d'une
  sous-requête, lire le SQL produit → [[une-sous-requete-qualifie-la-colonne-exterieure]].
- Un filtre de statut s'écrit en liste blanche → [[une-enumeration-de-champs-se-teste]].
- Les tests qui manipulent des dates tournent avec un fuseau fixé (`TZ=UTC`).
- Un lot qui écrit sur les vraies données s'essaie sur un élément ; un chemin se découpe par `basename` / `dirname` → [[un-lot-qui-ecrit-sur-les-vraies-donnees-s-essaie-sur-un-seul-element]].
- Refaire des sorties pour propager un changement : savoir si le générateur lit la source ou une copie figée, et chercher le changement dans la sortie → [[refaire-depuis-une-copie-figee-ne-reprend-pas-la-source]].
- Texte généré par un modèle en série : après toute consigne de style, compter ouvertures et formules sur le lot entier ; un élément facultatif du moule est vide par défaut → [[un-tic-de-generation-se-mesure-sur-la-serie-pas-sur-le-texte]].

## Tenue à jour

Si une tâche introduit un patron réutilisable, **l'écrire dans le doc de
conventions dans la même tâche**. Une convention qui ne vit que dans le code est
une convention que personne ne suivra.
