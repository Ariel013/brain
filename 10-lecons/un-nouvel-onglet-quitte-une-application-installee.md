---
titre: Dans une application installée (PWA), un nouvel onglet quitte l'application — un document s'ouvre dedans
type: lecon
origine: FIBDA Bodybuilding — 2026-09-26
tags: [pwa, mobile, session, impression]
---

# Dans une application installée (PWA), un nouvel onglet quitte l'application — un document s'ouvre dedans

**Symptôme.** Jour de la compétition : « impossible d'imprimer, ça disparaît
quand je clique sur Imprimer ». Sur l'ordinateur du développeur, le même lien
ouvrait proprement la version imprimable dans un onglet.

**Cause.** L'application est installée sur l'écran d'accueil du téléphone
(`display: standalone`). Un lien `target="_blank"` n'y ouvre pas un onglet :
il **bascule vers le navigateur**, dans un contexte qui n'a pas le cookie de
session de l'application. L'utilisateur voit son application disparaître et,
au mieux, une page « non connecté ». Rien de tout cela n'apparaît en test sur
un navigateur de bureau, où l'onglet partage la session.

**Règle.** Dans une application qui peut être installée, **rien ne s'ouvre dans
un autre onglet**. Un document imprimable se récupère avec la session
(`fetch` + cookie), s'affiche dans un cadre pleine page à l'intérieur de
l'application, s'imprime depuis ce cadre (`contentWindow.print()`), et se
referme d'un bouton. Un `<base href>` injecté dans le document fait résoudre
ses liens relatifs (logo) sur l'origine de l'application.

**Corollaire.** Tout `target="_blank"` d'un projet PWA est un défaut en
attente : le chercher (`grep _blank`) avant la mise en ligne.

Voir [[regarder-l-application-fait-partie-de-la-recette]],
[[un-garde-fou-local-se-leve-hors-ligne]].
