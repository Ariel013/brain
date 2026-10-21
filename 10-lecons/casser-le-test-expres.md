---
titre: Un test de garde se vérifie en cassant le code exprès
type: lecon
origine: Synoé — 2026-08-25 · Optimisation CV — 2026-10-20
tags: [tests]
---

# Un test de garde se vérifie en cassant le code exprès

**Symptôme.** Un test écrit **après** le correctif passe au vert. Il ne prouve
rien : il passe au vert pour de mauvaises raisons aussi souvent que pour les
bonnes.

**Cause.** Un test n'atteste que de ce qu'il exerce réellement. Écrit sur un
code déjà réparé, rien ne dit qu'il touche le chemin réparé.

**Règle.** Retirer la ligne corrigée et **voir le test échouer en nommant la
bonne chose**. C'est le seul moment où l'on sait ce qu'il garde.

**Variantes du même piège.**
- Un test d'isolation qui ne peut pas échouer ne prouve rien : le valider par
  mutation (casser la règle, constater le rouge).
- Se méfier d'un `expect(0 ligne)` seul — zéro ligne peut venir d'un chemin
  inexistant plutôt que de la règle testée. Doubler d'un contrôle négatif qui,
  lui, réussit.

**Occurrence — un test vert sans sa garde (Optimisation CV, 2026-10-20).** Le
test « une phrase de fermeture cachée dans un `<script>` ne compte pas » passait
même garde retirée : la phrase de l'essai ne correspondait à aucun motif du
code, donc elle n'était jamais trouvée, script ou pas. Seule la mutation l'a
montré. Corollaire : **la donnée d'essai d'un test de garde doit déclencher le
motif sans la garde** — sinon il teste l'absence de correspondance, pas la garde.

Voir aussi [[une-enumeration-de-champs-se-teste]], [[verifier-le-chemin-d-ecriture]].
