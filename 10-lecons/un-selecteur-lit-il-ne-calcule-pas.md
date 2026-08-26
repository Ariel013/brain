---
titre: Un sélecteur lit, il ne calcule pas
type: lecon
origine: Synoé — 2026-08-23
tags: [etat, front]
---

# Un sélecteur lit, il ne calcule pas

**Symptôme.** `useStore((s) => s.maListe ?? [])` a tué trois écrans d'un coup :
« Maximum update depth exceeded ». Ni les 476 tests métier ni le typecheck ne
pouvaient le voir.

**Cause.** Le repli rend un tableau **neuf à chaque appel**. Le store ne mémoïse
plus les sélecteurs, la comparaison se fait par référence, l'état semble changer
à chaque rendu, et la boucle part.

**Règle.** Un sélecteur **lit**. Pas de `?? []`, pas de `.map`, pas de
`.filter`, pas de littéral.
- Si la valeur peut manquer, c'est **l'état** qu'on complète à l'entrée.
- Si elle doit être calculée, c'est **dans l'écran**, mémoïsée.

**Corollaire, plus large.** Un **type optionnel traversé par une frontière change
de sens** : optionnel au stockage (un enregistrement ancien n'a pas la clé
récente), obligatoire en mémoire. Écrire **les deux types** plutôt qu'un seul et
des replis partout.

Voir aussi [[un-seul-etat-derive-le-reste]].
