---
titre: Leçons apprises
aliases: [Leçons, MOC Leçons]
type: index
maj: 2026-10-21
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
- [[refuser-plutot-que-convertir]] — une conversion silencieuse est une donnée fausse ; 0 n'est presque jamais une mesure
- [[normaliser-a-la-lecture]] — deux unités dans un même champ se convertissent à la lecture
- [[un-seul-etat-derive-le-reste]] — deux états qui doivent s'accorder sont un seul état mal nommé
- [[un-selecteur-lit-il-ne-calcule-pas]] — un sélecteur qui construit sa valeur fait boucler le rendu
- [[lire-le-fichier-reel-avant-de-modeliser]] — la structure est dans les répétitions, pas les en-têtes
- [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]] — 57 pools ouverts pour 3 requêtes
- [[retirer-une-regle-devant-un-repli-fait-tomber-le-cas-dans-le-repli]] — pour exclure un cas, ajouter la règle qui l'écarte
- [[un-refus-partage-le-predicat-de-ce-qu-il-protege]] — un refus qui compte avec un autre critère que la lecture compte zéro là où elle compte un
- [[une-ecriture-brute-ne-trace-pas-l-action-publique-oui]] — journaliser dans l'action du magasin, jamais dans l'écran ; l'écriture composée reste muette
- [[une-appartenance-s-ecrit-elle-ne-se-derive-pas-ecran-par-ecran]] — un rattachement dérivé dans un seul écran : « 0 dossier » ailleurs ; et jamais d'écriture dans un recalcul (hors journal)
- [[un-test-qui-porte-la-formule-la-protege]] — l'attendu de caisse soustrayait deux fois la monnaie, et le test portait la formule fausse dans son titre
- [[une-regle-opposable-n-a-pas-de-valeur-par-defaut]] — `ordonnance` absent valait « vente libre » : un champ qui porte une obligation est obligatoire, le défaut est le plus restrictif
- [[une-modification-envoie-ce-qui-a-change-pas-l-etat]] — 🔴 chaque sauvegarde renvoyait tout le cabinet, chaque appareil relisait tout : quota Supabase sauté ; delta dès la v1, et le coût réseau se chiffre avant
- [[une-reference-ajoutee-relance-le-test-de-suppression-de-la-table-visee]] — une clé étrangère ajoutée a cassé l'effacement RGPD de la veille ; tester la suppression avec une ligne liée
- [[une-frontiere-de-mot-en-francais-s-ecrit-avec-les-lettres-accentuees]] — `^r\b` reconnaissait « Rédaction » ; `(?<![\p{L}\d])…(?![\p{L}\d])` avec `u`, et mesurer le dictionnaire sur les vraies données
- [[un-nom-exact-n-est-pas-une-identite]] — « EDF », « Siemens » : l'unique nom exact d'un annuaire était une coquille homonyme ; une preuve de plus que le nom
- [[une-sous-requete-qualifie-la-colonne-exterieure]] — Drizzle écrit `"id"` dans un SELECT : la sous-requête le captait, compte faux sans erreur

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
- [[un-verrou-se-livre-avec-sa-voie-de-correction]] — retirer un geste dangereux engage à livrer le geste sûr, le même jour
- [[un-nouvel-onglet-quitte-une-application-installee]] — en PWA installée, `target="_blank"` bascule vers le navigateur sans la session
- [[un-champ-masque-cache-l-espace-colle]] — « Code incorrect » sur tous les appareils : un espace collé, invisible
- [[une-proposition-s-affiche-elle-ne-se-preselectionne-pas]] — une catégorie présélectionnée faisait entrer au CV ce qu'on voulait seulement apprendre

## Vérifier

- [[casser-le-test-expres]] — un test de garde se prouve en le faisant échouer
- [[regarder-l-application-fait-partie-de-la-recette]] — 480 tests verts, trois écrans blancs
- [[mesurer-l-outil-avant-de-conclure]] — un outil se vérifie dans le régime où on l'emploie
- [[une-sauvegarde-se-verifie-avant-de-detruire]] — la taille d'un fichier ne prouve rien
- [[un-test-de-route-emprunte-le-chemin-de-l-ecran]] — 64 tests verts, la restauration impossible depuis l'écran
- [[un-tri-sur-une-colonne-castee-trie-sur-le-cast]] — un jeu d'essai à un chiffre ne teste pas un tri
- [[un-budget-de-poids-est-une-contrainte-de-perimetre]] — mesurer le socle vide avant d'écrire
- [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]] — un drapeau désarme le contrôle que le script promet
- [[des-tests-qui-n-ecrivent-jamais-ne-protegent-pas-les-ecritures]] — 82 tests verts, trois écritures qui plantent au deuxième appel
- [[un-test-se-borne-a-son-propre-jeu-de-donnees]] — une requête sans filtre touche les données réelles en silence
- [[lire-la-donnee-avant-l-hypothese]] — un rapport donne un effet et une cause : garder l'effet, lire la base
- [[une-garde-lit-le-texte-sous-la-forme-ou-il-sera-rendu]] — le contrôle lisait le texte sans balisage : aucun lien jamais vu, alors que le PDF les rendait

## Git, release, agents

- [[stager-nommement]] — une commande large ne regarde pas ce qu'elle ramasse
- [[un-espace-partage-se-verifie-propre-avant-d-y-ecrire]] — ne jamais committer ce qu'on n'a pas écrit
- [[une-release-se-coupe-sur-un-perimetre]] — pas sur l'état de `dev`
- [[une-fonction-serverless-s-envoie-regroupee-et-se-verifie-au-curl]] — « Aliased » trois fois, l'API morte trois fois
- [[l-inscription-a-une-offre-gratuite-se-fait-avant-l-adr]] — l'ADR écrit, le fournisseur exige un paiement
- [[verifier-chaque-commit-du-decoupage]] — ne jamais affirmer ce qu'on n'a pas mesuré
- [[nommer-la-copie-visee]] — `git -C <copie>` dès le second worktree
- [[chercher-avant-d-ecrire]] — grepper le domaine, pas le nom du fichier envisagé
- [[ecrire-la-decision-avec-le-code]] — un ADR écrit après n'est jamais écrit
- [[une-conclusion-consignee-devient-consigne]] — corriger le doc fait partie du correctif
- [[un-rapport-d-agent-est-une-piste-pas-un-fait]] — un constat qui fonde une décision se revérifie à la source
- [[un-worktree-d-agent-part-de-main-pas-de-la-branche-courante]] — nommer le commit de base dans le brief, le faire vérifier en première commande
- [[avant-de-retirer-un-garde-fou-lister-ce-que-l-operation-ecrit]] — une borne retirée « parce que ce n'est pas le vecteur » rouvrait le registre des stupéfiants
- [[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]] — 8 constats élevés sur du code à 100 % de tests verts ; chaque constat reproduit, corrigé avec un test avant/après
- [[arreter-un-processus-par-son-pid-pas-par-un-motif]] — `pkill -f "next dev"; suite` s'est tué lui-même : la suite n'a jamais eu lieu

## Sécurité et résilience

- [[la-cle-d-administration-ne-va-jamais-cote-client]]
- [[un-garde-fou-local-se-leve-hors-ligne]] — un verrou sur des données locales se lève hors ligne
- [[un-acte-porte-son-auteur-pas-son-transporteur]] — hors ligne, celui qui synchronise n'est pas celui qui a agi ; un identifiant de session n'est pas un secret
- [[le-client-n-est-jamais-une-autorite]] — chaque champ d'une charge utile est une donnée, un calcul ou une autorité ; le serveur recalcule
- [[un-acte-passe-se-juge-sur-des-faits-dates-jamais-sur-un-etat-courant]] — une vente hors ligne refusée à vie parce que la session avait été purgée depuis
- [[un-echec-temporaire-ne-consomme-pas-de-tentative]] — une nuit hors ligne faisait abandonner la première vente de la file
- [[une-cle-un-usage-un-texte-signe-dit-a-quoi-il-sert]] — un registre signé par la clé des jetons meurt à la première rotation
- [[un-garde-fou-trop-large-empeche-sa-propre-documentation]] — un filtre décide sur ce qui s'exécute, pas sur ce qui s'écrit
- [[un-rapport-qui-signale-une-donnee-sensible-ne-la-recopie-pas]] — le contrôle final se fait sur `git log -p`, pas sur le disque
- [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]] — changer de niveau plutôt qu'affaiblir le garde
- [[publier-un-detail-en-tout-ou-rien-et-le-tester-en-lecteur-qui-connait-la-regle]] — chaque cas particulier de masquage était une fuite ; tout ou rien, et énumérer les mondes possibles
- [[un-garde-fou-qui-compte-zero-par-invisibilite-n-est-pas-un-garde-fou]] — un garde-fou vérifie d'abord qu'il voit ; au moins un fichier de tests sous le rôle de production
- [[un-mecanisme-de-detection-se-teste-en-continuant-apres-la-detection]] — altérer, détecter, puis laisser tourner le cycle suivant ; « ignoré » n'est jamais un verdict
- [[une-action-irreversible-a-trois-issues-faite-pas-faite-incertaine]] — « rien n'est parti » après une coupure ou une erreur de base : un renvoi doublait l'e-mail ; l'incertain bloque la répétition
- [[un-lien-venu-d-une-donnee-se-controle-sur-l-adresse-resolue]] — `localhost.` et un nom public vers 127.0.0.1 passaient le filtre de texte ; contrôler l'adresse résolue à chaque redirection

---

## Comment en ajouter une

Le jour où l'erreur est corrigée, pas plus tard. Une note, un titre qui **est la
règle** (pas le sujet), et le triptyque symptôme → cause → règle. Puis un lien
depuis cet index et depuis la note de méthode concernée.

Le test d'admission : *est-ce que je voudrais qu'on me le rappelle sur un projet
qui n'a rien à voir ?* Si non, ça reste dans le `JOURNAL.md` du projet.
