---
titre: Un maintien en vie ne dépend pas de l'activité qu'il est censé remplacer
type: lecon
origine: NearYou (GéoService) — 2026-10-22
tags: [hebergement, supabase, github-actions, cron]
---

# Un maintien en vie ne dépend pas de l'activité qu'il est censé remplacer

**Symptôme.** Le projet Supabase gratuit s'est retrouvé en pause alors qu'un
workflow GitHub planifié le « pingait » deux fois par semaine depuis fin juin.
Il a fallu restaurer l'ancien projet et migrer la base vers un autre compte.

**Cause.** GitHub désactive les workflows planifiés d'un dépôt après 60 jours
sans activité sur le dépôt. Le dernier commit datait du 29 juin : le ping s'est
arrêté fin août, et Supabase a mis le projet en pause une semaine plus tard.
Le garde-fou ne tournait que tant que le projet vivait — exactement la
situation où il ne sert à rien. *(Cause établie par les dates et la règle
documentée de GitHub ; l'état « disabled » du workflow n'a pas été relu dans
l'onglet Actions.)*

**Règle.** Un mécanisme qui maintient un service en vie s'héberge sur une
plateforme qui tourne **sans** activité du projet — ici, un cron de
l'hébergeur de l'application (Vercel Cron, quotidien) qui fait une vraie
lecture en base. Le cron GitHub reste au mieux un secours.

**Corollaire.** Pour tout « keep-alive », se demander : *qu'est-ce qui l'arrête,
et est-ce que ça arrive précisément quand le projet dort ?* Et le vérifier
par son effet (dernière exécution réussie), pas par sa présence dans le dépôt.

Voir [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]], [[l-inscription-a-une-offre-gratuite-se-fait-avant-l-adr]].
