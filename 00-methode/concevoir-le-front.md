---
titre: Concevoir le front sans se casser la tête
aliases: [Front, Design, UI]
type: methode
maj: 2026-10-24
---

# Concevoir le front sans se casser la tête

> Le front se **décide** avant de se coder. Un écran codé sans contexte produit
> l'interface générique que tout modèle sait faire : bleu SaaS, cartes
> identiques, mobile étiré sur un écran d'ordinateur. Ce qui l'évite, c'est
> deux fichiers posés tôt et un brief validé avant chaque surface.

## Les quatre outils et leur rôle

| Outil | Rôle | Autorité |
|---|---|---|
| **impeccable** (skill) | Méthode de design : `teach` → `shape` → `craft`, puis `critique`, `audit`, `polish`, `adapt`… Lois anti-« fait par une IA ». | **Fait foi.** En cas de désaccord, impeccable tranche. |
| **ui-ux-pro-max** (skill) | Base de données consultable : 119 règles UX, recommandations par stack (Next, shadcn, Three…), polices, types de graphiques. | **Référence à consulter**, jamais une consigne. Son générateur de design system propose des palettes en hex génériques : ne pas l'appliquer tel quel. |
| **skillui** (CLI `npx skillui`) | Extrait le design system d'un site existant (couleurs, typo, espacements) en `DESIGN.md`. | Seulement quand j'ai **un site qui m'inspire**. Sortie dans le scratchpad, relue, puis fondue dans le `DESIGN.md` du projet. |
| **playwright-cli** (skill + CLI) | Ouvrir l'app, capturer, cliquer, à 375 / 768 / 1440 px. Plus sobre en contexte que le MCP Playwright. | Preuve visuelle de la recette → [[regarder-l-application-fait-partie-de-la-recette]] |

Versions et installation : [[claude-code]].

## Le déroulé

1. **À l'amorce** — répondre aux questions front (ci-dessous), puis
   `impeccable teach` écrit `PRODUCT.md` : qui, pour quoi, personnalité,
   anti-références, accessibilité. **Register** : `product` (l'app sert une
   tâche) ou `brand` (le design est le produit).
2. **Dès qu'il y a du code** — `impeccable document` écrit `DESIGN.md` depuis
   les vrais tokens. Une charte existante se **reprend et s'améliore**, elle ne
   se jette pas → [[un-vas-y-sur-un-audit-ne-vaut-pas-refonte]].
3. **Avant chaque surface** — `impeccable shape` : un brief (scène d'usage,
   mise en page mobile **et** desktop, états vides, mouvement) que je
   **valide** avant la première ligne. Pas de code sans brief validé.
4. **Pendant** — `ui-ux-pro-max` pour une question précise (« bottom sheet
   accessible », « carte + liste en Next »), une requête par intention.
5. **Avant le rapport** — capture playwright-cli aux trois largeurs, et
   `npx impeccable detect src/` (62 règles déterministes, sans IA).

## Les questions front de l'amorce

À poser en une salve, avec les questions de [[amorce-nouveau-projet]] :

1. **Sur quoi l'utilise-t-on surtout ?** Téléphone, ordinateur, les deux — et
   si les deux : l'ordinateur a-t-il sa **vraie mise en page** (jamais le
   mobile étiré) ?
2. **Trois mots de personnalité.**
3. **Un site ou une app dont tu aimes l'allure**, et ce qui te plaît dedans.
   Si oui → `skillui`. Si non → impeccable propose, je choisis.
4. **Ce que ça ne doit surtout pas ressembler.**
5. **Qui est l'usager le plus contraint** : téléphone d'entrée de gamme,
   connexion lente, plein soleil, aisance de lecture.
6. **Une charte existe-t-elle déjà** (couleurs, logo, polices) ?

## Ce qui se décide une fois

- **Mobile d'abord, desktop pensé** : dès qu'une app vise le téléphone, le
  desktop reçoit sa propre mise en page dans le même lot, pas « plus tard ».
- **Chaque état a son écran** : vide, chargement, erreur, zéro résultat. Un
  « 0.0 (0) » est un état vide non conçu.
- **Une dépendance visuelle lourde** (carte WebGL, 3D, animation) est un choix
  structurant → ADR, avec son repli.

Voir [[amorce-nouveau-projet]], [[recette-avant-release]],
[[une-fonctionnalite-invisible-est-absente]].
