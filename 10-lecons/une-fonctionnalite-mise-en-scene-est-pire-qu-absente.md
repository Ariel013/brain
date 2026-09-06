---
titre: Une fonctionnalité mise en scène est pire qu'absente
type: lecon
origine: Kalybris — 2026-09-05
tags: [maquette, gouvernance, recette]
---

# Une fonctionnalité mise en scène est pire qu'absente

**Symptôme.** Un prototype affichait un bandeau : « MODE OFFLINE — Toutes vos
actions sont enregistrées localement · **Reprise auto** au retour du réseau »,
suivi de « Dernière sync : il y a 4 min ». Les deux phrases étaient fausses.
L'audit a trouvé **zéro occurrence** de la moindre API réseau du navigateur dans
31 000 lignes : pas de service worker, pas de file d'attente, pas d'écouteur de
reconnexion. Et « il y a 4 min » était une **chaîne de caractères littérale**,
adossée à aucun horodatage — aucune variable ne stockait de date de
synchronisation nulle part.

**Cause.** Une maquette dessine ce que la fonctionnalité *aura l'air* d'être.
Rien dans l'outil de maquettage ne distingue l'écran qui affiche un état calculé
de celui qui affiche un texte écrit à la main. Les deux se ressemblent
exactement — et le second est plus facile à produire.

**Règle.** Toute promesse faite à l'écran (« enregistré », « synchronisé »,
« validé par le pharmacien », « anonymisé », « chiffré ») se vérifie en
**remontant jusqu'au code qui la tient**. Si on ne le trouve pas, ce n'est pas
une remarque de recette : c'est un défaut bloquant.

**Pourquoi c'est pire qu'une absence.** Une fonctionnalité absente se voit et
se planifie. Une fonctionnalité **mise en scène** est vue par le décideur, qui
en conclut raisonnablement que le sujet est traité, et qui construit un planning
dessus. Le coût n'est pas technique, il est de gouvernance — et il se paie
plusieurs mois plus tard, au moment où le sujet devait être derrière soi.

**Le geste concret.** Quand une démo sert de base à une décision, produire le
tableau « ce que l'écran montre / ce que le code fait », ligne par ligne, et le
faire lire à qui décide du planning. C'est le seul document qui rétablit la
vérité sans dévaloriser le travail de maquette, qui, lui, garde toute sa valeur.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]],
[[regarder-l-application-fait-partie-de-la-recette]],
[[une-fonctionnalite-invisible-est-absente]].
