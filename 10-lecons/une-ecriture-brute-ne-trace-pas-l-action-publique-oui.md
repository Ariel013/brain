---
titre: Une écriture brute ne trace pas, l'action publique oui
type: lecon
origine: Synoé — 2026-10-08
tags: [audit, store, architecture]
---

# Une écriture brute ne trace pas, l'action publique oui

**Symptôme.** Pour fermer une dette (l'import créait des dossiers sans ligne
au journal d'audit, deux modales modifiaient sans trace, une troisième
traçait en double), la journalisation a été descendue dans l'action du
magasin `majSalarie`. Un test a aussitôt cassé : « journalise une fois ».
Six autres actions du magasin (pièces jointes, photo, classement)
**réutilisaient `majSalarie` comme écriture brute** et traçaient déjà leur
propre acte — elles auraient désormais écrit deux lignes par geste.

**Cause.** Une même fonction servait deux rôles : l'**acte** que l'écran
déclenche (qui doit tracer) et l'**écriture** qu'une autre action compose
(qui ne doit pas tracer, c'est l'action composante qui trace).

**Règle.** Dans une couche qui journalise, **séparer l'écriture brute de
l'action publique** : une fonction interne qui écrit et ne trace jamais
(`ecrireDossier`), une action exportée qui écrit **et** trace. Les actions
du magasin composent la première ; les écrans n'appellent que la seconde,
et ne journalisent jamais eux-mêmes — sinon chaque nouvel écran choisit
s'il trace, et l'un d'eux oublie.

**Corollaire.** Le test « une ligne par geste » est celui qui révèle le
double rôle. Le garder, et l'écrire pour chaque action qui compose
une écriture.

Voir aussi [[un-seul-etat-derive-le-reste]], [[verifier-le-chemin-d-ecriture]].
