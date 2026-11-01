---
titre: Un journal d'audit se pose avec la première écriture
type: lecon
origine: Synoé, 2026-08
tags: [securite, donnees]
---

# Un journal d'audit se pose avec la première écriture

**Symptôme.** Le journal d'audit a été branché après les premiers dossiers
réels. Il ne raconte donc pas le début : qui a créé, consulté ou modifié ces
dossiers-là reste inconnu.

**Cause.** L'audit avait été vu comme une fonctionnalité à ajouter plus tard,
alors que sa valeur tient à ce qu'il couvre **depuis le premier jour**.

**Règle.** Sur des données sensibles, le journal d'audit (acteur, action, cible,
horodatage) est branché **dans la même tâche que la première écriture de donnée
métier**. Posé tard, il est irrattrapable.

Voir aussi [[une-ecriture-brute-ne-trace-pas-l-action-publique-oui]],
[[revue-securite]].
