---
titre: Revue de sécurité
aliases: [Revue sécurité, Security audit]
type: methode
maj: 2026-10-20
---

# Revue de sécurité

Chaque fonctionnalité passe une revue de sécurité **avant son rapport de
tâche**. L'outil : le skill `security-audit` de Cloudflare, installé dans
`~/.claude/skills/security-audit/` (source et version :
[[claude-code]]).

> Des tests verts ne prouvent pas l'absence de contournement : le
> contournement vit à côté de la règle testée
> → [[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]].

## Deux modes, deux moments

Le skill distingue lui-même deux modes. Le choix du mode se dit
**explicitement** dans la consigne : sans précision, le skill pose une question
au lieu de démarrer.

| Moment | Mode | Périmètre | Ce qu'il produit |
|---|---|---|---|
| **Chaque fonctionnalité** | *guidance* | le diff de la tâche et les chemins qu'il touche | des constats dans la conversation, aucun fichier |
| **Avant une release** | *full audit*, profil `quick` (ou `standard` si le périmètre touche auth, argent, santé, registre) | le dépôt, ou le diff `main..dev` en run *scoped* | `REPORT.md`, `findings.json` dans `~/security-audit-skill/<repo>/run-<N>` |

Le *full audit* lance de nombreux sous-agents : il ne se lance pas par
fonctionnalité. Une demande d'« audit » sans précision de mode est une demande
de *guidance*.

## Par fonctionnalité

1. Une fois le code écrit et les tests verts, **avant** le rapport : revue du
   diff avec le skill en mode *guidance*.
2. Si le diff touche l'authentification, les données sensibles, les politiques
   d'accès, l'argent, la santé ou l'import/export, la revue est faite par **un
   autre agent** (`security-reviewer`) que celui qui a écrit le code, avec
   consigne de chercher le contournement — pas de valider la règle.
3. Un constat ne compte que s'il nomme la frontière franchie, le principal
   affecté et le résultat (exigence du skill). Une bonne pratique manquante
   n'est pas un constat.
4. Un constat élevé se corrige **dans la tâche**, avec un test qui le
   reproduit avant la correction → [[casser-le-test-expres]].
5. Le résultat monte dans la ligne **Sécurité** du rapport
   → [[rapport-de-tache]].

## Avant une release

Étape de [[recette-avant-release]]. Le rapport du run est **lu** — tous les
`confirmed` traités ou reportés par une décision écrite, chaque
`needs_validation` assigné. Un run *quick* ou *scoped* se dit partiel : il
n'atteste rien du reste du dépôt.

## Ce que le skill ne fera pas ici

- **Exécuter le code cible sans sandbox.** Le skill n'exécute rien hors d'un
  bac à sable du système (pas de réseau, environnement vide, limites). Sous
  WSL, sans ce bac à sable, la revue reste statique et ce qui demande une
  exécution sort en `needs_validation`. C'est voulu : ne pas le contourner.
- **Tester un déploiement réel.** Pas de sonde sur une URL en ligne, un compte
  réel ou une donnée réelle.
- **Recopier une donnée sensible dans un rapport**
  → [[un-rapport-qui-signale-une-donnee-sensible-ne-la-recopie-pas]].

## Points à chercher dans un diff (ajoutés le 2026-10-21)

- Le code ouvre un lien venu d'une donnée → [[un-lien-venu-d-une-donnee-se-controle-sur-l-adresse-resolue]].
- Une garde contrôle un texte nettoyé alors que le rendu interprète le balisage
  → [[une-garde-lit-le-texte-sous-la-forme-ou-il-sera-rendu]].
- Une action irréversible (envoi, paiement) dit « échec » sur toute erreur
  → [[une-action-irreversible-a-trois-issues-faite-pas-faite-incertaine]].
- Une référence ajoutée vers une table qui porte un droit d'effacement
  → [[une-reference-ajoutee-relance-le-test-de-suppression-de-la-table-visee]].

Voir aussi [[travailler-avec-les-agents]].
