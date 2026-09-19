---
titre: Une conversion silencieuse est une donnée fausse
type: lecon
origine: Synoé — 2026-08-23 · Strongman — 2026-09-20
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

**Seconde occurrence — une borne qui commence à 0 accepte « rien » comme une
valeur (Strongman, 2026-09-20).** Une performance était bornée de 0 à 100 000.
Or le logiciel avait un état dédié pour « pas de performance » : le verdict
Zéro, valeur vide, hors classement. Une épreuve annulée a été soldée en tapant
« 0 » partout : vingt-et-un athlètes « à 0 m » ont été classés, départagés au
poids de corps, et ont marqué des points. Rien n'a été converti, cette fois —
mais deux façons de dire « rien » coexistaient, et le calcul n'en comprenait
qu'une. **Quand un état dédié existe pour « rien », la valeur numérique qui
dit la même chose se refuse, avec un message qui nomme l'état à utiliser.**
« Borner au vraisemblable » inclut la borne basse : 0 n'est presque jamais une
mesure.

Voir aussi [[normaliser-a-la-lecture]], [[ce-que-l-ecran-promet-le-code-le-fait]],
[[un-seul-etat-derive-le-reste]], [[lire-la-donnee-avant-l-hypothese]].
