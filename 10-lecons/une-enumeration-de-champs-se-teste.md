---
titre: Une énumération de champs est un piège à retardement
type: lecon
origine: Synoé — 2026-08-23
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

Voir aussi [[verifier-le-chemin-d-ecriture]].
