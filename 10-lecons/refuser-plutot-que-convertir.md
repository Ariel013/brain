---
titre: Une conversion silencieuse est une donnée fausse
type: lecon
origine: Synoé — 2026-08-23
tags: [donnees, saisie]
---

# Une conversion silencieuse est une donnée fausse

**Symptôme.** `Number('')` vaut 0. `parseInt('12 boîtes')` vaut 12. Deux façons
d'accepter en silence ce qu'il fallait refuser.

**Cause.** Le langage convertit au jugé, et le code s'en remet à lui. Sur une
donnée qui compte, **la valeur fausse est pire que l'absente** : l'absence se
voit, la fausse valeur se lit comme une mesure.

**Règle.** Une saisie se **contrôle et se refuse**, jamais ne se convertit au
jugé. Pas de `?? 0`, pas de `|| valeurPrécédente`, pas de champ ignoré. Et
**borner au vraisemblable** : une faute de frappe produit souvent un nombre
parfaitement bien formé (« 700 » pour « 70 »).

**Corollaire.** Contrôler partout ne veut pas dire **bloquer** partout. Une
valeur aberrante en général peut être la bonne dans un cas précis (« 185 » est un
numéro d'urgence). Et ce qui est volontairement du texte libre doit le rester :
le contraindre fait perdre de l'information.

Voir aussi [[normaliser-a-la-lecture]], [[ce-que-l-ecran-promet-le-code-le-fait]].
