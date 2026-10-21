---
titre: Une garde lit le texte sous la forme où il sera rendu, pas sous sa forme nettoyée
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [securite, controle, rendu]
---

# Une garde lit le texte sous la forme où il sera rendu, pas sous sa forme nettoyée

**Symptôme.** Les corrections de Kevin sur son CV passaient un contrôle qui
devait signaler tout lien nouveau. Le contrôle lisait `sansBalisage(texte)` —
le texte où `[libellé](url)` est réduit à son libellé. Aucun lien n'était
donc jamais vu, alors que le gabarit les rendait en liens cliquables dans le
PDF, `javascript:` et chemins locaux compris.

**Cause.** Le nettoyage sert à comparer des mots ; il retire précisément ce que
la garde devait voir. Le texte contrôlé n'était pas le texte rendu.

**Règle.** Chaque garde lit le texte **tel que le rendu l'interprétera**. Si
le rendu interprète un balisage (liens, HTML, formules), la garde voit le
balisage. Et le rendu se défend aussi lui-même (ici : un lien n'est émis
qu'en `http(s)` ou `mailto`).

Voir [[un-lien-venu-d-une-donnee-se-controle-sur-l-adresse-resolue]], [[un-garde-fou-trop-large-empeche-sa-propre-documentation]].
