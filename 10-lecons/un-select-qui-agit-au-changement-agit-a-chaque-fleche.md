---
titre: Un select qui agit au changement agit à chaque flèche
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [interface, clavier, accessibilite]
---

# Un select qui agit au changement agit à chaque flèche

**Symptôme.** Liste « Nationalité(s) » : choisir un pays l'ajoutait à la liste, puis le sélecteur revenait à vide. À la souris, tout allait bien. Au clavier, trois appuis sur Flèche bas ajoutaient Afghanistan, Afrique du Sud et Albanie. Taper « Cot » ajoutait Cambodge, Colombie et Côte d'Ivoire.

**Cause.** Sur un `<select>` fermé, chaque flèche ou lettre change la valeur et déclenche `change`. Le gestionnaire traitait chaque `change` comme une décision définitive : ajouter, puis remettre à zéro. Une navigation au clavier devenait une suite d'actions.

**Règle.** Un `<select>` porte une valeur ; il ne déclenche pas d'action. Pour une liste multiple, mettre un sélecteur par élément, plus un bouton « Ajouter ». Une flèche change alors la valeur courante, elle n'ajoute rien.

**Corollaire.** Tout contrôle de formulaire relié à un effet (ajout, navigation, envoi) se teste au clavier, flèches comprises, pas seulement au clic.

Voir aussi [[un-champ-qui-ne-s-envoie-qu-avec-entree-est-bloque-sur-telephone]], [[une-proposition-s-affiche-elle-ne-se-preselectionne-pas]].
