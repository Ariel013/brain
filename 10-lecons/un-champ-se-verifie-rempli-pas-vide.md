---
titre: Un champ de formulaire se vérifie rempli, pas seulement vide
type: lecon
origine: UKWC — 2026-11-11
tags: [front, recette, formulaire]
---

# Un champ de formulaire se vérifie rempli, pas seulement vide

**Symptôme.** Page d'inscription livrée après captures mobile et desktop
regardées : rendu fidèle à la maquette. Le client écrit dans le champ
Instagram : son texte passe **sous** le « @ » décoratif.

**Cause.** Le « @ » était posé en `absolute` par-dessus l'input, avec un
`pl-10` (Tailwind) pour lui laisser la place. Une classe scoped du composant
fixait `padding: 0 1.25rem` et l'emportait : le texte démarrait sous le
préfixe. **À vide, rien ne se voyait** — et toutes les captures avaient été
prises formulaire vide, ou remplies sur d'autres champs.

**Règle.**
- Les captures de recette d'un formulaire incluent **chaque champ rempli**,
  avec une valeur de longueur réaliste.
- Un préfixe ou un suffixe visuel (`@`, `+229`, `€`) se pose dans un **groupe
  flex bordé** (préfixe + input sans bordure), jamais en absolu sur l'input :
  le texte ne peut alors pas passer dessous, quel que soit le padding gagnant.

Voir [[regarder-l-application-fait-partie-de-la-recette]],
[[un-indicatif-prerempli-dans-un-champ-telephone-est-ecrase-par-l-autoremplissage]].
