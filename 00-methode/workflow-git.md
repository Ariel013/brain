---
titre: Workflow git
aliases: [Git, Branches, Release]
type: methode
maj: 2026-08-26
---

# Workflow git

## La règle absolue

**Jamais de `git push` sans confirmation explicite, à chaque fois.** Ce n'est
pas une autorisation qui se donne une bonne fois : elle se redemande avant
*chaque* push, y compris en fin de longue session, y compris si un push a déjà
été validé une heure plus tôt.

Le reste des commandes git — branche, `add`, `commit`, fusion locale, tag —
l'agent les exécute lui-même. Il annonce ce qu'il fait.

## Hiérarchie de branches

```
main       ← PRODUCTION. Reçoit uniquement staging, et seulement quand on est sûr.
 └ staging  ← RECETTE. Candidat stable, miroir de la prochaine prod. Le filet AVANT.
    └ dev    ← INTÉGRATION. C'est ici qu'on teste et qu'on vérifie tout.
       └ <type>/<slug>  ← une branche par tâche, issue de dev.
```

- **Jamais de commit direct** sur `main`, `staging`, `dev` : elles ne reçoivent
  que des fusions.
- **Une tâche = une branche = un sujet.** Si une tâche s'avère en couvrir
  plusieurs, le signaler et proposer un découpage **avant** de coder.
- **Remontée un niveau à la fois**, testée à chaque niveau. On ne saute pas.
- `type` ∈ `feat`, `fix`, `refactor`, `docs`, `chore`, `test`, `style`. Le plus
  précis, jamais `chore` par facilité.

## Promotion et release

- La promotion `dev → staging → main` se fait **en local** (fusions non-FF +
  tag, puis push). **Pas de PR web `dev→main`** : doubler les deux fait diverger
  `origin/main` et oblige à réconcilier à chaque release.
- Avant de pousser `main` : rattraper `origin/main` en **fast-forward** si
  besoin, et vérifier `git diff main dev` **vide** avant de taguer.
- **Jamais de `reset --hard` sur une branche partagée.** Un reset a déjà fait
  perdre des commits et déplacé un tag. Pour rattraper : `merge --ff-only`.
- **Taguer chaque release** (`v1.0`, `v1.1`…). Le tag est l'ancre de rollback —
  pas `staging`, qui peut déjà porter la version *suivante*, moins éprouvée.
  `staging` est le filet *avant* la prod ; le tag est le filet *après*.
- Une release se coupe sur **un périmètre décidé**, pas sur l'état de `dev`
  → [[une-release-se-coupe-sur-un-perimetre]].

## Séquence d'une tâche

1. Lire les docs que `CLAUDE.md` désigne pour le sujet.
2. Brancher `<type>/<slug>` depuis un `dev` à jour.
3. Coder.
4. Vérifier : typecheck, tests, **et regarder l'application**
   → [[regarder-l-application-fait-partie-de-la-recette]].
5. Produire le [[rapport-de-tache]].
6. `git add <chemins nommés>` puis `git commit` → [[stager-nommement]].
7. Après validation : remontée `dev` → `staging` → `main`, un niveau à la fois.
   **Confirmation explicite avant chaque push.**
8. Mettre à jour `A-FAIRE.md` si une action manuelle est apparue, cocher la
   tâche dans le backlog, mettre à jour `JOURNAL.md`.

## Format de commit

```
<type>: <résumé court à l'impératif>

<corps optionnel : le POURQUOI, pas le quoi, si le diff ne suffit pas>
```

**Ne jamais écrire dans un message de commit une propriété qu'on n'a pas
mesurée.** « Chaque commit compile » est une affirmation qui survit à l'erreur
→ [[verifier-chaque-commit-du-decoupage]].

## Worktrees

Dès qu'un second worktree existe, **préfixer toute commande d'écriture par
`git -C <copie>`** — tag, commit, merge. Et vérifier le résultat par ce qu'il
pointe (`git rev-parse v<tag>^{commit}`), pas par le fait que la commande n'a
pas protesté. → [[nommer-la-copie-visee]]

Le worktree est aussi ce qui permet de découper, vérifier et releaser **sans
arrêter le serveur de développement** — on ne bascule jamais de branche sous la
copie qui sert le dev.

## Ce qu'on ne fait jamais silencieusement

- Modifier un schéma de base sans le signaler dans le rapport de tâche.
- Toucher à l'authentification, au stockage de documents ou aux données
  sensibles sans avoir relu les règles de conformité **juste avant**.
- Ajouter une dépendance externe sans le mentionner — chaque dépendance est une
  surface de plus à maintenir et à sécuriser.
