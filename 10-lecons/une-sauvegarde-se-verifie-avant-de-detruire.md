---
titre: Une sauvegarde se vérifie avant de détruire, pas après
type: lecon
origine: Synoé — 2026-08
tags: [ops, donnees]
---

# Une sauvegarde se vérifie avant de détruire, pas après

**Symptôme.** Un fichier de sauvegarde chiffré de ~86 octets. Autrement dit : un
dump vide, produit par une commande qui a échoué **en laissant son fichier**.

**Règle.** Une sauvegarde se vérifie en la **déchiffrant et en comptant les
lignes attendues**, avant toute opération destructive. **La taille du fichier ne
prouve rien.**

**Trois pièges qui vont avec :**
- **Un échec ne doit pas laisser de fichier.** Écrire en `.partiel`, renommer
  seulement en cas de succès — sinon un échec produit un artefact qui a l'air
  d'une sauvegarde.
- **Un dump de base ne couvre pas le stockage de fichiers.** Les documents ne
  sont dans aucune sauvegarde par défaut : les exporter avant toute purge, ou
  les perdre.
- **Après une remise à zéro, vider le stockage local du navigateur.** L'app
  garde des données locales et une session sur un compte qui n'existe plus — on
  croit à un bug.

Voir aussi [[une-conclusion-consignee-devient-consigne]].
