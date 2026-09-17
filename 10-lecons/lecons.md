---
titre: Leçons apprises
aliases: [Leçons, MOC Leçons]
type: index
maj: 2026-09-17
---

# Leçons apprises

> Une note par règle **payée par une erreur réelle**. Format : symptôme → cause
> → règle. Le symptôme est décrit tel qu'il s'est présenté, pas tel qu'on le
> comprend après coup — c'est sous cette forme qu'on le recroisera.

**À lire avant de coder sur n'importe quel projet.** Ce n'est pas une formalité :
la moitié de ces règles ont été payées par un défaut parti en production.

## Données et état

- [[verifier-le-chemin-d-ecriture]] — une donnée qui vit à l'écran n'est pas une donnée enregistrée
- [[une-enumeration-de-champs-se-teste]] — toute liste explicite de champs prend du retard
- [[refuser-plutot-que-convertir]] — une conversion silencieuse est une donnée fausse
- [[normaliser-a-la-lecture]] — deux unités dans un même champ se convertissent à la lecture
- [[un-seul-etat-derive-le-reste]] — deux états qui doivent s'accorder sont un seul état mal nommé
- [[un-selecteur-lit-il-ne-calcule-pas]] — un sélecteur qui construit sa valeur fait boucler le rendu
- [[lire-le-fichier-reel-avant-de-modeliser]] — la structure est dans les répétitions, pas les en-têtes
- [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]] — 57 pools ouverts pour 3 requêtes

## Frontières et architecture

- [[le-calcul-sort-de-l-ecran]] — un composant ne contient que du rendu
- [[isoler-la-persistance-derriere-un-contrat]] — les écrans ne connaissent jamais la base
- [[poser-l-isolation-des-le-premier-schema]] — le cloisonnement coûte une colonne au jour 1

## Ce que l'utilisateur voit

- [[ce-que-l-ecran-promet-le-code-le-fait]] — l'écart entre l'affirmation et le calcul
- [[une-fonctionnalite-invisible-est-absente]] — un état vide muet se lit comme une panne
- [[une-propriete-de-colonne-ne-survit-pas-a-une-rangee]] — quand un conteneur tourne, relire ses enfants
- [[une-fonctionnalite-mise-en-scene-est-pire-qu-absente]] — une maquette qui promet ce qu'aucun code ne tient
- [[une-consigne-executable-se-redige-contre-le-code]] — une consigne fausse produit un faux négatif
- [[un-champ-qui-se-resynchronise-ecrase-la-frappe-en-cours]] — la valeur du serveur ne reprend la main qu'au repos

## Vérifier

- [[casser-le-test-expres]] — un test de garde se prouve en le faisant échouer
- [[regarder-l-application-fait-partie-de-la-recette]] — 480 tests verts, trois écrans blancs
- [[mesurer-l-outil-avant-de-conclure]] — un outil se vérifie dans le régime où on l'emploie
- [[une-sauvegarde-se-verifie-avant-de-detruire]] — la taille d'un fichier ne prouve rien
- [[un-tri-sur-une-colonne-castee-trie-sur-le-cast]] — un jeu d'essai à un chiffre ne teste pas un tri
- [[un-budget-de-poids-est-une-contrainte-de-perimetre]] — mesurer le socle vide avant d'écrire
- [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]] — un drapeau désarme le contrôle que le script promet
- [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]] — 82 tests verts, trois écritures qui plantent au deuxième appel
- [[un-test-se-borne-a-son-propre-jeu-de-donnees]] — une requête sans filtre touche les données réelles en silence

## Git, release, agents

- [[stager-nommement]] — une commande large ne regarde pas ce qu'elle ramasse
- [[un-espace-partage-se-verifie-propre-avant-d-y-ecrire]] — ne jamais committer ce qu'on n'a pas écrit
- [[une-release-se-coupe-sur-un-perimetre]] — pas sur l'état de `dev`
- [[verifier-chaque-commit-du-decoupage]] — ne jamais affirmer ce qu'on n'a pas mesuré
- [[nommer-la-copie-visee]] — `git -C <copie>` dès le second worktree
- [[chercher-avant-d-ecrire]] — grepper le domaine, pas le nom du fichier envisagé
- [[ecrire-la-decision-avec-le-code]] — un ADR écrit après n'est jamais écrit
- [[une-conclusion-consignee-devient-consigne]] — corriger le doc fait partie du correctif
- [[un-rapport-d-agent-est-une-piste-pas-un-fait]] — un constat qui fonde une décision se revérifie à la source

## Sécurité et résilience

- [[la-cle-d-administration-ne-va-jamais-cote-client]]
- [[un-garde-fou-local-se-leve-hors-ligne]] — un verrou sur des données locales se lève hors ligne
- [[un-garde-fou-trop-large-empeche-sa-propre-documentation]] — un filtre décide sur ce qui s'exécute, pas sur ce qui s'écrit
- [[un-rapport-qui-signale-une-donnee-sensible-ne-la-recopie-pas]] — le contrôle final se fait sur `git log -p`, pas sur le disque
- [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]] — changer de niveau plutôt qu'affaiblir le garde

---

## Comment en ajouter une

Le jour où l'erreur est corrigée, pas plus tard. Une note, un titre qui **est la
règle** (pas le sujet), et le triptyque symptôme → cause → règle. Puis un lien
depuis cet index et depuis la note de méthode concernée.

Le test d'admission : *est-ce que je voudrais qu'on me le rappelle sur un projet
qui n'a rien à voir ?* Si non, ça reste dans le `JOURNAL.md` du projet.
