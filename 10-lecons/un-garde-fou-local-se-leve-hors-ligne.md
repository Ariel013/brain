---
titre: Une porte qui ne s'ouvre que depuis l'extérieur enferme
type: lecon
origine: Synoé — 2026-08-23
tags: [securite, resilience]
---

# Une porte qui ne s'ouvre que depuis l'extérieur enferme

**Symptôme.** Un verrou de session vérifiait le mot de passe **auprès du
serveur**. Le jour où le service d'authentification s'est tu, l'utilisatrice
s'est retrouvée dehors — devant des données **locales**, sur **sa** machine,
sans délai d'attente, sans message, et sans aucun recours dans l'application.

**Cause.** Un garde-fou posé sur des données locales avait été câblé sur une
dépendance distante.

**Règle.** Tout garde-fou posé sur des données **locales** doit pouvoir se lever
**hors ligne**. Et tout appel réseau dont dépend un écran doit avoir un **délai**
et un **message distinct** pour « le serveur ne répond pas » — jamais le message
du refus, qui envoie l'utilisateur chercher une faute inexistante.

**Corollaire de surveillance.** **Surveiller une moitié d'un service rassure à
tort.** Le keep-alive interrogeait la base, qui allait très bien, et aurait
déclaré le système sain pendant toute la panne. Une sonde doit couvrir **ce dont
l'usage dépend réellement** — ici, se connecter.

Voir aussi [[ce-que-l-ecran-promet-le-code-le-fait]].
