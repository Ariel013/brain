---
titre: La clé d'administration ne va jamais côté client
type: lecon
origine: Synoé — 2026-08
tags: [securite]
---

# La clé d'administration ne va jamais côté client

**Règle.** Une clé qui **contourne les règles d'accès** ne va jamais dans un
bundle front — un bundle est public, quel que soit le domaine qui le sert. Toute
fonction d'administration qui en dépend est soit **locale**, soit derrière une
**fonction serveur**.

**Ce qui va avec, sur le contrôle d'accès :**

- **Droit d'accès ≠ politique.** Une nouvelle table peut avoir des politiques
  impeccables et rester **morte** faute de droit accordé au rôle applicatif. Et
  l'inverse est pire : un droit sans politique ouvre tout.
- **Distinguer les refus.** Lecture interdite = lignes masquées **sans erreur**.
  Contrainte d'écriture violée = **erreur**. Condition qui ne matche rien =
  **0 ligne touchée, sans erreur**. Rôle sans droit = *permission denied*, en
  amont de tout le reste. Confondre les quatre fait chercher au mauvais endroit.
- **Un refus avorte la transaction** : dans un test qui enchaîne plusieurs refus
  attendus, encadrer chaque requête d'un point de reprise.
- **Un test d'isolation qui ne peut pas échouer ne prouve rien**
  → [[casser-le-test-expres]].

Voir aussi [[poser-l-isolation-des-le-premier-schema]],
[[un-garde-fou-local-se-leve-hors-ligne]].
