---
titre: Un champ qui se resynchronise depuis le serveur écrase la frappe en cours
type: lecon
origine: Strongman — 2026-09-17
tags: [front, saisie, latence]
---

# Un champ qui se resynchronise depuis le serveur écrase la frappe en cours

**Symptôme.** « Quand on remplit un champ, ça se supprime ou déconne, il faut
réécrire plusieurs fois. » Un nom tapé d'une traite perdait sa fin. En local,
rien à voir.

**Cause.** Le champ s'enregistrait tout seul après une pause de frappe, et la
page revenait rafraîchie du serveur avec la valeur enregistrée. Le composant
adoptait cette valeur dès qu'elle changeait — or elle change précisément parce
qu'on vient d'envoyer une **version partielle** du texte. Tant que
l'aller-retour tient dans la pause, on ne voit rien ; dès qu'il la dépasse
(connexion réelle, serveur lointain), chaque texte un peu long est tronqué.

**Règle.** Un champ contrôlé à enregistrement automatique n'adopte la valeur
du serveur qu'**au repos** : curseur sorti, aucun envoi en vol, aucune frappe
en attente. Trois états, pas un « si la valeur a changé ».

**Corollaire.** Une saisie automatique se **teste sur la latence réelle**, pas
sur le poste de développement où l'aller-retour est instantané. Le défaut
n'existe pas en local — il est systématique en ligne.

Voir aussi [[une-fonctionnalite-invisible-est-absente]], [[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]] (même famille : ce qui ne se voit qu'en production), [[regarder-l-application-fait-partie-de-la-recette]].
