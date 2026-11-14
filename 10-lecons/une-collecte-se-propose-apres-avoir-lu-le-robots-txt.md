---
titre: Une collecte se propose après avoir lu le robots.txt et ce que le site envoie de lui-même
type: lecon
origine: Optimisation CV — 2026-11-12
tags: [collecte, scraping, conformite]
---

# Une collecte se propose après avoir lu le robots.txt et ce que le site envoie de lui-même

**Symptôme.** Pour « récupérer chaque jour toutes les offres », la lecture
automatique d'un site d'emploi (HelloWork) a été proposée à l'utilisateur.
En la préparant : son `robots.txt` interdit la page de recherche, toute
adresse à paramètres et les pages d'offres ; son plan du site renvoie une page
de blocage. La piste proposée était interdite dès le départ.

**Cause.** La faisabilité a été pensée côté technique (« on peut lire la
page ») avant de regarder ce que le site permet. Même famille d'erreur la
semaine précédente sur le même projet : une démarche demandée à l'utilisateur
pour une API absente du catalogue.

**Règle.** Avant de proposer de lire un site : lire son `robots.txt` et ses
conditions, et chercher ce qu'il **envoie de lui-même** (API publique, flux,
alertes e-mail). La proposition faite à l'utilisateur ne contient que des
voies permises. Ici, les alertes e-mail que les sites envoient à
l'utilisateur, lues dans sa propre boîte, ont remplacé la lecture des sites.

Voir [[l-inscription-a-une-offre-gratuite-se-fait-avant-l-adr]], [[ecrire-la-decision-avec-le-code]].
