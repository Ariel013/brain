---
titre: Un champ conditionnel masqué se purge, il ne se cache pas
type: lecon
origine: FIBDA CONNECT — 2026-11-10
tags: [donnees, formulaire, minimisation]
---

# Un champ conditionnel masqué se purge, il ne se cache pas

**Symptôme.** Profil d'une Ivoirienne, région, commune et quartier remplis. On retire la nationalité ivoirienne : les trois champs disparaissent de l'étape « Représentation ». Pourtant, le récapitulatif affichait toujours « Rattachement en Côte d'Ivoire : … », et le dossier partait avec. Même chose pour un mineur redevenu majeur : responsable légal et autorisation restaient en mémoire. Les tests n'avaient rien vu ; une relecture adverse l'a trouvé.

**Cause.** La condition (« nationalité ivoirienne », « mineur ») décidait seulement de l'affichage. La donnée saisie quand la condition était vraie n'était jamais retirée quand elle devenait fausse. Le formulaire a deux états : ce qui est montré, ce qui est gardé. Seul le premier suivait la règle.

**Règle.** Toute règle d'affichage conditionnel a sa fonction de purge, dans la couche métier, appliquée à chaque validation d'étape et à l'envoi. Une donnée qu'on ne peut plus voir ni corriger n'a pas le droit de partir.

**Corollaire.** Le test se fait en deux temps : remplir sous la condition, la retirer, puis vérifier ce qui est réellement envoyé ou affiché au récapitulatif. Il ne suffit pas de constater que le champ n'est plus à l'écran.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]], [[verifier-le-chemin-d-ecriture]], [[un-seul-etat-derive-le-reste]].
