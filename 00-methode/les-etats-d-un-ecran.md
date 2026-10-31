---
titre: Les onze états d'un écran
aliases: [États d'écran, Empty state, Loading state, Error state]
type: methode
maj: 2026-10-31
---

# Les onze états d'un écran

> Un écran n'a pas un état, il en a onze. Celui qu'on dessine est le cas
> heureux ; les dix autres arrivent quand même, et si personne ne les a
> conçus, l'usager les reçoit bruts : un écran blanc, un spinner sans fin, un
> « Error 500 », un formulaire qui refuse sans dire quoi. **Chaque état se
> conçoit avec la surface, dans le même lot** — pas « plus tard ».

## Les onze, et ce que chacun doit faire

| État | Ce qu'il doit faire | Le défaut qu'il évite |
|---|---|---|
| **Vide** | Dire **pourquoi** c'est vide (rien encore, filtre trop strict, rien d'autorisé) et donner **la prochaine action** (un bouton, pas une phrase). | « 0 élément », « 0.0 (0) », une liste nue. |
| **Chargement** | Montrer **la forme** de la page qui arrive (squelette, légère animation de pulsation), à la place exacte du contenu. Pas de spinner seul au centre. | Le saut de mise en page, l'attente sans repère. |
| **Erreur** | Dire **ce qui n'a pas marché**, **à qui la faute** (vous, le réseau, nous) et **comment s'en sortir** (réessayer, corriger, contacter). Rien de technique à l'écran ; le détail va au rapport d'assistance. | « Une erreur est survenue », le code d'erreur brut. |
| **Hors ligne** | Ne **jamais** laisser un écran blanc : afficher ce qui est déjà connu, dire qu'on est hors ligne, ce qui marche encore, et ce qui partira au retour du réseau. | L'écran blanc, la saisie perdue. |
| **Réseau lent** | Montrer **l'avancée** (étape en cours, proportion, ce qui est déjà arrivé) plutôt qu'une attente opaque ; afficher le partiel dès qu'il existe. | L'usager qui recharge et perd tout. |
| **Aucun résultat** | Dire « aucun résultat pour *X* », puis **proposer** : orthographe proche, filtre à retirer, recherche plus large. | L'impasse, le sentiment d'avoir cassé l'outil. |
| **Accès refusé** | Expliquer **pourquoi** (rôle, compte, périmètre) et donner **une route de retour** (accueil, se connecter avec un autre compte, demander l'accès). Sans révéler ce qui est caché. | L'écran vide qui ressemble à un bug, ou la fuite de l'existence de la donnée. |
| **Page introuvable (404)** | Une vraie page : dire que l'adresse ne mène nulle part, proposer l'accueil et les entrées principales. Garder l'habillage de l'application. | La page blanche du serveur, l'impasse hors application. |
| **Session expirée** | **Sauvegarder le travail en cours avant** de déconnecter (brouillon local), le dire, et le **restituer** après reconnexion. | Le formulaire de vingt minutes perdu. |
| **Validation de formulaire** | Afficher l'erreur **en ligne, sur le champ fautif**, avec la correction attendue ou **un exemple** (« 06 12 34 56 78 »). Au moment où l'usager quitte le champ ou envoie, pas à chaque frappe. Le focus va au premier champ fautif. | Le bandeau rouge en haut qui ne dit pas quel champ. |
| **Succès** | **Confirmer** ce qui a été fait (avec l'objet : « Dossier de M. X enregistré »), **rassurer** (c'est sauvegardé, envoyé, synchronisé) et **montrer la suite** (l'action suivante probable). | Le silence après le clic, le doute qui fait cliquer deux fois. |

## Comment l'appliquer

- **Au brief de chaque surface** (`impeccable shape`, [[concevoir-le-front]]) :
  le brief liste les onze et dit, pour chacun, soit son écran, soit pourquoi
  il ne peut pas arriver ici. Un état « sans objet » s'écrit, il ne s'oublie
  pas.
- **Composants partagés, une fois** : un état vide, un squelette, un bloc
  d'erreur, un bandeau hors ligne, une page 404, un message de champ. Chaque
  écran les compose ; personne ne réécrit son propre « chargement… ».
- **Le texte se rédige comme un contenu**, dans la langue de l'usager : qui,
  quoi, quoi faire. Pas de jargon technique, pas d'excuse vague.
- **La recette les provoque** : couper le réseau, ralentir la connexion
  (profil « 3G lente »), vider la base de test, saisir faux, expirer la
  session, viser une adresse inexistante, se connecter avec un rôle restreint
  → [[recette-avant-release]]. Un état jamais provoqué n'est pas vérifié
  → [[regarder-l-application-fait-partie-de-la-recette]].
- **Accessibilité** : un message d'erreur ou de succès est annoncé (région
  `aria-live`) ; un squelette porte `aria-busy` ; l'animation respecte
  `prefers-reduced-motion`.

## Pourquoi c'est une règle de méthode

Un état non conçu, c'est l'application qui parle à la place du concepteur —
et elle parle mal. Et ce sont précisément les moments où l'usager est le plus
fragile (perdu, bloqué, pressé, hors réseau) : c'est là que se perd ou se gagne
sa confiance. Voir aussi [[une-fonctionnalite-invisible-est-absente]].
