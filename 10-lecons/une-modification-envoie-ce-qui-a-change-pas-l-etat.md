---
titre: Une modification envoie ce qui a changé, jamais l'état entier
type: lecon
origine: Synoé — 2026-10-13
tags: [donnees, reseau, synchro, cout, architecture]
---

# Une modification envoie ce qui a changé, jamais l'état entier

**Symptôme.** Bandeau Supabase : « Organization exceeded its quota… Projects
will be restricted from 06 Nov ». Page Usage : egress 6,95 Go pour 5 Go inclus,
**952 393 messages temps réel pour 3 utilisateurs** et 5 connexions au plus,
alors que la base pèse 31 Mo. Le plan Pro n'est pas payable à ce moment-là : la
restriction (réponses 402, synchronisation coupée) tombera sur le pilote.

**Cause.** Le chemin d'écriture avait été conçu comme « l'état du client fait
foi » : chaque sauvegarde (320 ms après la dernière frappe) réécrivait le bloc
cabinet **et les 231 dossiers**, inchangés compris. Pour Postgres, un `upsert`
à l'identique est une modification : chaque ligne produisait une notification
temps réel, envoyée à **chaque** appareil abonné — l'auteur compris — avec la
ligne entière ; puis chaque appareil **relisait tout le cabinet**. Une frappe =
~700 messages portant un dossier médical + 3 lectures complètes.

Le risque était **écrit** dans un ADR deux mois plus tôt (« tant que sauvegarder
signifie réécrire le monde… ») et reporté à « la normalisation ». Personne n'en
avait chiffré le coût : octets × fréquence × appareils, contre le quota du plan.
Les tests étaient verts — ils vérifient la justesse, jamais le volume.

**Règle.**
1. **Dès la première version**, un chemin d'écriture envoie le **delta** : les
   lignes (ou champs) qui diffèrent de ce que le serveur tient. Rien n'a changé
   → aucun appel réseau.
2. Une notification **s'applique** (la ligne reçue), elle ne déclenche pas une
   relecture complète ; l'écho de sa propre écriture est ignoré. La relecture
   complète est un **secours** (suppression, reconnexion, ligne tronquée).
3. Avant de valider un design réseau, **écrire le calcul** : taille × fréquence
   × appareils, par mois, rapporté au quota du plan (egress, messages temps
   réel). Un chiffre qui approche le quota au pilote explosera en production.
4. « On le fera à la normalisation » sur un chemin d'écriture n'est pas un
   report gratuit : c'est une dette qui se paie en quota, et en écrasements
   entre appareils (le même mécanisme renvoyait des copies périmées).

**Corollaire.** Une relecture de code qui ne pose que « est-ce juste ? » laisse
passer « combien ça coûte ? ». Les relectures d'un chemin réseau posent les deux.

**Corollaire bis.** Le correctif n'efface pas le cycle déjà consommé : sur un
plan gratuit, la marge se perd en un jour d'emballement et ne se rattrape pas.
Surveiller la page d'usage **pendant** le pilote, pas après le bandeau.

Voir aussi [[verifier-le-chemin-d-ecriture]],
[[isoler-la-persistance-derriere-un-contrat]],
[[un-cache-seulement-en-developpement-est-absent-la-ou-il-compte]],
[[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]].
