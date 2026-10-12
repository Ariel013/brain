---
titre: Une appartenance s'écrit, elle ne se dérive pas écran par écran
type: lecon
origine: Synoé — 2026-10-12
tags: [modele, coherence, journal-audit, correctif]
---

# Une appartenance s'écrit, elle ne se dérive pas écran par écran

**Symptôme.** Les rapports d'une entreprise affichaient zéro salarié : les
dossiers ouverts avant que leur site soit rattaché à l'entreprise n'avaient pas
d'`entrepriseId`. Premier correctif : dans les rapports, « l'entreprise du
dossier, sinon celle de son site ». La relecture a montré que l'écran
d'administration affichait alors « 0 dossier » pour cette entreprise (et
invitait à la supprimer), que le filtre de la liste disait 0, et que la fiche
d'entreprise contredisait ses propres totaux — le même dossier compté ici,
absent là.

**Cause.** Le correctif créait une **seconde définition** de l'appartenance,
lue par un seul écran ; tous les autres gardaient la première. Une dérivation à
la lecture doit être appelée par chaque lecteur, et un seul oubli refait
l'écart.

**Règle.** Une donnée d'appartenance (site, entreprise, équipe…) **s'écrit**
dans l'enregistrement, par une action qui trace chaque enregistrement modifié,
et tous les écrans la lisent telle quelle. Les cas qui la font bouger
(rattacher un site, retirer une entreprise) passent par la même action et
emmènent leurs enregistrements.

**Corollaire — pas d'écriture dans un recalcul.** Ce rattrapage, d'abord placé
dans la fonction qui reconstruit l'état à chaque lecture, modifiait des
dossiers **sans aucune trace au journal d'audit** (une trace y aurait été
répétée à chaque lecture). Toute modification d'un enregistrement passe par une
action explicite, déclenchée une fois, et journalisée.

Voir aussi [[un-seul-etat-derive-le-reste]],
[[une-ecriture-brute-ne-trace-pas-l-action-publique-oui]],
[[un-selecteur-lit-il-ne-calcule-pas]].
