---
titre: Une énumération de champs est un piège à retardement
type: lecon
origine: Synoé — 2026-08-23 · Strongman — 2026-09-17 · Synoé — 2026-10-04
tags: [donnees, tests]
---

# Une énumération de champs est un piège à retardement

**Symptôme.** Une structure énumérait les clés qui partent vers le serveur. Une
tâche a ajouté un champ sans l'y inscrire : jamais écrit, et comme le distant
l'emporte à l'hydratation, la donnée aurait disparu de l'écran **sans erreur ni
bruit**. Le compilateur ne dit rien : les clés sont optionnelles.

**Cause.** Partout où du code **énumère** des champs au lieu de les **dériver**
— sérialisation, export, formulaire, mapping — la liste prend du retard sur la
source de vérité. Une seconde copie d'une liste explicite diverge toujours.

**Règle.** Deux niveaux :
1. **Dériver plutôt qu'énumérer** quand c'est possible : un seul chemin, les
   autres l'appellent.
2. Quand l'énumération est inévitable, **poser un test qui la compare à la
   source de vérité** (`Object.keys` du type contre les clés rangées) — puis
   [[casser-le-test-expres]] pour vérifier qu'il parle.

**Corollaire.** Une clé optionnelle ajoutée à un type partagé est un endroit à
auditer, pas une addition anodine : `?` fait taire le compilateur exactement là
où on aurait besoin qu'il crie.

**Seconde occurrence — un message qui énumère des états (Strongman, 2026-09-17).**
Un passage avait trois états. Un quatrième, « en attente de résultat », a été
ajouté avec ses tests. Le message de « Reconstruire l'ordre » disait encore
« tous les passages sont déjà validés » : il énumérait implicitement les états
finaux, et le nouveau n'y était pas. L'utilisateur l'a lu comme un bug — des
athlètes manquaient « sans raison ». Même règle : quand on ajoute un état,
**grepper chaque message et chaque `statut ===` qui raisonne sur la liste**,
pas seulement les filtres qui ont fait échouer un test.

**Troisième occurrence — une préférence qui énumère ce qui est affiché (Synoé,
2026-10-04).** Le réglage « quelles courbes afficher » gardait, par dossier, la
liste des courbes **cochées**. Une cinquième courbe (le pouls) a été ajoutée :
sur tout dossier déjà réglé, elle naissait décochée — donc invisible, exactement
le symptôme qu'on venait corriger. Relevé en relecture, avant livraison. Même
cause : une liste explicite ne connaît que ce qui existait le jour où elle a été
écrite. **Une préférence stocke l'exception, pas la totalité** : ce que
l'utilisateur a masqué, pas ce qu'il voit. Le nouveau venu est alors visible par
défaut, sans migration. Et l'ancien réglage se convertit contre la liste **telle
qu'elle était quand il a été écrit**, pas contre celle d'aujourd'hui.

Voir aussi [[verifier-le-chemin-d-ecriture]], [[une-fonctionnalite-invisible-est-absente]].
