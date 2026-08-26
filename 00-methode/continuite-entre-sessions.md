---
titre: Continuité entre sessions
aliases: [Continuité, JOURNAL, Reprise]
type: methode
maj: 2026-08-26
---

# Continuité entre sessions

Le problème : chaque nouvelle conversation avec un agent repart **froide**. Sans
dispositif, elle re-explore le dépôt, refait des choix déjà tranchés, et refait
les mêmes erreurs. Le `JOURNAL.md` est le dispositif.

## Les trois règles

1. **Reprise sans relecture du code.** Lire `JOURNAL.md` puis `CLAUDE.md` doit
   suffire à savoir où on en est et quoi faire. Si ça ne suffit pas, c'est le
   journal qui est en défaut, pas l'agent.
2. **Apprendre de ses erreurs.** Toute erreur commise **et corrigée** est
   consignée en « Leçons apprises ». C'est ce qui rend l'instance suivante
   meilleure que la précédente.
3. **Être force de proposition.** Après avoir pris l'état, proposer les
   prochaines étapes utiles — en **recommandant**, pas en listant des options.

## Les trois sections du JOURNAL

**📍 État actuel & prochaine action** — daté, factuel, court. Ce qui est en
production, ce qui est aligné avec le distant (vérifié par SHA, pas supposé), ce
qui reste en attente. Toujours convertir les dates relatives en absolues :
« hier » ne veut rien dire dans trois semaines.

**📓 Journal des sessions** — une entrée datée par session : ce qui a été fait,
ce qui a été décidé, ce qui a été découvert.

**🎓 Leçons apprises** — le trésor. Format **symptôme → cause → règle**. On
décrit le symptôme *tel qu'il s'est présenté* (« trois écrans blancs », pas
« bug de sélecteur »), parce que c'est sous cette forme qu'on le recroisera.

## Ce qui reste dans le projet, ce qui monte dans le brain

| Reste dans `JOURNAL.md` | Monte dans le [[README|brain]] |
|---|---|
| L'état, les versions, les prochaines actions | — |
| Une leçon liée à une bibliothèque ou un schéma précis | Une leçon vraie pour **le projet suivant** |
| Un piège d'outillage propre à ce dépôt | Une règle de méthode générale |

Le test : *est-ce que je voudrais qu'on me le rappelle sur un projet qui n'a
rien à voir ?* Si oui → `10-lecons/`. Sinon → le journal du projet.

## Le danger du journal

**Une conclusion consignée devient une consigne pour l'instance suivante.** Un
faux diagnostic écrit dans le journal se transmet et oriente le travail à côté.
Corriger le document fait donc partie de la correction du défaut — pas d'un
nettoyage ultérieur. → [[une-conclusion-consignee-devient-consigne]]

## Fin de session

Trois gestes, jamais négociables :
1. Mettre à jour « État & prochaine action ».
2. Ajouter l'entrée datée au journal des sessions.
3. Consigner les leçons — puis lancer `/capitaliser` pour faire remonter ici ce
   qui dépasse le projet.
