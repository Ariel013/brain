---
titre: Un texte scellé se sérialise sans ambiguïté
type: lecon
origine: Kalybris — 2026-10-19 (revue) · 2026-11-01 (correctif)
tags: [securite, cryptographie, signature, integrite]
---

# Un texte scellé se sérialise sans ambiguïté

**Symptôme.** Le registre des stupéfiants scellait (HMAC chaîné) et signait
(RS256) chaque ligne sur ses champs **joints par un séparateur invisible**
(U+001F), réputé « absent de tout texte saisi ». Faux : rien ne le refusait
dans les champs libres. Un prescripteur saisi `Dr X␟<uuid>` donnait la même
chaîne jointe qu'un autre prescripteur suivi d'un autre pharmacien : un
administrateur de base pouvait réattribuer une dispensation de stupéfiant
**sans casser ni le sceau, ni la signature, ni la chaîne**. La vérification
répondait « intacte ». Même défaut pour les champs facultatifs : `''` et
`null` se confondaient.

**Cause.** Le sceau prouve que *la chaîne* n'a pas changé, pas que *les
champs* n'ont pas changé. Une jointure par séparateur n'est injective que si
le séparateur ne peut apparaître dans aucun champ — hypothèse qu'aucun code
ne tenait.

**Règle.** Ce qu'on scelle ou signe est une **sérialisation injective** des
champs : tableau JSON canonique (échappe les contrôles, distingue `null` de
`''`, nombre de champs fixe) ou préfixe de longueur — jamais une jointure.
La sérialisation porte **sa version en tête**, et la ligne stocke la version
avec laquelle elle a été scellée : on peut alors corriger le format sans
réécrire ce qui est déjà scellé, et refuser un retour à l'ancien format.
Une jointure existante n'est tolérable qu'avec **au plus un champ libre**,
invariant écrit au-dessus du code et tenu par un test qui casse si un
second apparaît.

**Ni refuser ni nettoyer à la réception.** Refuser le caractère bloquait à
jamais un acte hors ligne déjà encaissé ; le retirer en silence faisait
sceller autre chose que ce que l'auteur avait signé. Le défaut est dans le
format du sceau, c'est là qu'il se corrige.

**Faire avant les données réelles.** Les lignes déjà scellées dans l'ancien
format restent exposées pour toujours.

Voir [[une-cle-un-usage-un-texte-signe-dit-a-quoi-il-sert]],
[[refuser-plutot-que-convertir]], [[casser-le-test-expres]].
