---
titre: Un rapport qui signale une donnée sensible ne la recopie pas
type: lecon
origine: Kalybris — 2026-09-05
tags: [securite, donnees-personnelles, git, audit]
---

# Un rapport qui signale une donnée sensible ne la recopie pas

**Symptôme.** Un audit trouve des données personnelles dans un livrable tiers :
n° de sécurité sociale, salaires, une ordonnance nominative complète. Réaction
immédiate et correcte — geler le dossier dans `.gitignore` pour qu'il n'entre
jamais dans l'historique. Puis rédaction du rapport d'audit, avec chaque
constat **adossé à sa preuve littérale** : le nom de la patiente, sa date de
naissance, son numéro d'assurance, le nom du prescripteur et son numéro
d'ordre. Rapport committé. **La mesure de protection et la fuite étaient dans
la même session, à vingt minutes d'intervalle.**

**Cause.** Deux exigences légitimes qui tirent en sens inverse : « adosse
chaque constat à une preuve vérifiable » et « aucune donnée personnelle
n'entre dans le dépôt ». Le réflexe d'audit — citer littéralement — a satisfait
la première en faisant oublier la seconde. Le garde-fou avait été posé sur la
porte d'entrée, et la donnée est passée par le rapport qui la dénonçait.

**Règle.** Un document qui signale une donnée sensible en donne **la nature et
l'emplacement**, jamais la valeur. `fichier:ligne` suffit largement pour aller
vérifier : le rapport ne perd rien, et il cesse d'être lui-même une fuite.
Vaut pour un audit, un rapport de tâche, un message de commit, un ticket, un
journal de session, une capture d'écran.

**Ce qui l'a attrapée, et qui doit devenir systématique.** Un contrôle final
lancé *après* les commits : `git log -p` sur la plage des nouveaux commits,
grep sur une liste de motifs sensibles. Il ne figurait pas au plan, il a été
fait par acquit de conscience, et c'est lui qui a trouvé.

> Le contrôle final porte sur **`git log -p`, pas sur les fichiers du disque.**
> Les deux diffèrent dès qu'on a committé quelque chose qu'on a ensuite
> corrigé — et c'est précisément le cas qui compte.

**Le rattrapage n'a été possible que parce que rien n'était poussé.** Les
commits ont été réécrits (`--fixup`, puis rebase `--autosquash`). La règle
« jamais de push sans accord explicite » a couvert cette erreur-là par
accident : le délai qu'elle impose est aussi une fenêtre de rattrapage. C'est
un argument de plus en sa faveur, et il ne s'était encore jamais présenté sous
cette forme.

Voir aussi [[stager-nommement]], [[la-cle-d-administration-ne-va-jamais-cote-client]],
[[une-sauvegarde-se-verifie-avant-de-detruire]].
