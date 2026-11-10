---
titre: Un bouton qui apparaît sous le doigt reçoit le second appui
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [interface, mobile, double-clic, tests]
---

# Un bouton qui apparaît sous le doigt reçoit le second appui

**Symptôme.** Le test de double clic sur « Enregistrer mon inscription » passait à 768 et 1440 px. À 375 px, il échouait : après le double appui, l'écran de confirmation avait disparu et le formulaire était revenu vide à l'étape 1. Le serveur n'était pas en cause : il n'y en avait pas.

**Cause.** Le premier appui enregistrait et remplaçait le formulaire par l'écran de confirmation. Sur téléphone, son bouton « Recommencer » tombait exactement là où se trouvait « Enregistrer ». Le second appui, prévu pour le bouton qui venait de disparaître, a déclenché celui qui avait pris sa place. Le garde « une seule soumission » marchait ; c'est l'écran suivant qui n'était pas gardé.

**Règle.** Après une action qui remplace l'écran, le bouton qui apparaît à la place du précédent ignore les appuis pendant un court délai (une seconde ici), surtout s'il est destructif. Le focus et le défilement partent en haut de la nouvelle page.

**Corollaire.** Un test de double clic se lance à toutes les largeurs : la position des boutons, donc le défaut, dépend de la mise en page.

Voir aussi [[une-action-irreversible-a-trois-issues-faite-pas-faite-incertaine]], [[un-ecran-mobile-se-teste-a-la-hauteur-visible-pas-seulement-a-la-largeur]].
