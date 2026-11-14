---
titre: Une demande de fermeture se lit du côté de ce que voit le public
type: lecon
origine: UKWC — 2026-11-14
tags: [demande-client, intention, frontend]
---

# Une demande de fermeture se lit du côté de ce que voit le public

**Symptôme.** « Peut-on fermer les inscriptions à 12h ? » L'agent a répondu :
« aucun code à changer », il suffit de vider un réglage du `.env` de prod pour
que l'API refuse les inscriptions, et le formulaire affichera « fermé » après
envoi. Réponse de Kevin : « je veux juste remplacer sur la page le formulaire
par un truc du style inscriptions closes !!! ». Un aller-retour perdu, le jour
de l'événement, l'heure déjà passée.

**Cause.** La demande a été traduite en mécanisme (où se trouve l'interrupteur
dans le code) au lieu d'être lue comme un résultat attendu (ce que le visiteur
voit en arrivant). Avec la solution technique, le visiteur aurait encore vu un
formulaire ouvert, l'aurait rempli, puis aurait reçu un refus : exactement ce
que « fermer » voulait éviter.

**Règle.** Une demande d'ouvrir, de fermer, de masquer ou de désactiver se
traduit d'abord en **ce que voit le public** sur l'écran concerné. On livre
cet écran-là. La fermeture côté serveur vient en complément, jamais à la
place.

**Corollaire.** Quand la réponse tient en « rien à changer, il suffit de… »,
décrire ce que le visiteur verra après ce geste avant de la proposer. Si ce
n'est pas ce que le client a demandé, ce n'est pas la réponse.

Voir [[ce-que-l-ecran-promet-le-code-le-fait]], [[une-fonctionnalite-invisible-est-absente]].
