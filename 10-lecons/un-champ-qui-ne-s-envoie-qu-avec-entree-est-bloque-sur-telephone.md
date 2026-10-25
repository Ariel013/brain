---
titre: Un champ qui ne s'envoie qu'avec Entrée a besoin d'un bouton d'envoi sur téléphone
type: lecon
origine: CV interactif — 2026-10-25
tags: [front, mobile, formulaire, accessibilite]
---

# Un champ qui ne s'envoie qu'avec Entrée a besoin d'un bouton d'envoi sur téléphone

**Symptôme.** Mode terminal d'un CV web : sur son téléphone, Kevin tape une
commande et ne trouve aucun moyen de l'envoyer : « y'a pas de bouton
envoyer ». Sur ordinateur, tout marchait : tous les tests passaient au
clavier, avec Entrée.

**Cause.** Le formulaire n'avait que le champ, sans bouton : l'envoi reposait
sur la touche Entrée. Or le clavier virtuel ne montre pas toujours de touche
d'envoi claire. Les tests simulaient Entrée, que personne ne voit sur un
téléphone. Le même champ, en 14 px, faisait aussi zoomer iOS à la saisie.

**Règle.** Tout champ qui déclenche une action a un **bouton d'envoi
visible**, y compris quand l'interface imite un outil qui n'en a pas
(terminal, chat). Sur téléphone, `enterKeyHint` nomme la touche du clavier,
et le texte du champ fait au moins 16 px pour éviter le zoom d'iOS. Le test
de recette mobile **touche le bouton**, il ne presse pas Entrée.

Voir [[un-test-de-route-emprunte-le-chemin-de-l-ecran]],
[[concevoir-le-front]].
