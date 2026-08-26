---
titre: Isoler la persistance derrière un contrat
aliases: [Contrat Repo, Repo]
type: pattern
origine: Synoé — ADR 0002
maj: 2026-08-26
---

# Isoler la persistance derrière un contrat

**Le patron.** Une interface décrit *ce que l'application sait faire avec ses
données*. Deux implémentations au moins : une **locale**, toujours active, et une
**distante**, activée seulement si la configuration est renseignée. Les écrans ne
connaissent **que l'interface** — jamais la base, jamais le client distant.

```
        Écrans
          │
     contrat Repo
          │
   ┌──────┴──────┐
 local        distant
(toujours)   (si configuré)
```

**Ce que ça achète.**
- Développer et tester **sans compte** ni service externe.
- Un vrai mode hors ligne, pas un mode dégradé.
- Brancher plus tard une **troisième** implémentation (un vrai backend) sans
  toucher à un seul écran.

**La règle qui le maintient vivant.** Toute nouvelle capacité de données passe
par une **extension du contrat**, implémentée dans **les deux** backends — même
si l'un reste minimal au début. La première exception tue le patron : dès qu'un
écran appelle la base directement, l'interface n'est plus un contrat, c'est une
suggestion.

**Le corollaire qu'on oublie.** Une ressource distribuée par le contrat (URL
temporaire, abonnement, verrou) **se libère dans le contrat**, pas chez
l'appelant : plusieurs écrans la consomment et aucun ne sait quand les autres
ont fini.

Voir aussi [[conventions-de-code]], [[poser-l-isolation-des-le-premier-schema]].
