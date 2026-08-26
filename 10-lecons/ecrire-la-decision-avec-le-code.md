---
titre: Du code livré sans son ADR ni ses tests est une dette qui s'efface
type: lecon
origine: Synoé — 2026-08-24
tags: [agents, documentation, adr]
---

# Du code livré sans son ADR ni ses tests est une dette qui s'efface

**Symptôme.** Une instance a écrit 5 000 lignes — un module entier — et s'est
arrêtée **sans committer, sans tests, sans journal**. Le code **citait** un ADR
qui n'existait pas : la décision de fond ne vivait que dans un commentaire
d'en-tête, à un `git checkout` de disparaître. La reprise a coûté une session
entière de rétro-ingénierie de nos propres intentions.

**Cause.** La décision et le code qui l'applique ont été séparés dans le temps.
Le code survit ; le *pourquoi* s'évapore.

**Règle.** **Une décision structurante s'écrit dans le même mouvement que le code
qui l'applique**, pas après.

Et **un chantier ne se laisse pas dormir non committé** : le découpage se fait
tant que les intentions sont fraîches → [[verifier-chaque-commit-du-decoupage]].

**Signal à traiter immédiatement.** Un commentaire qui renvoie à un document
inexistant n'est pas une note de bonne intention : c'est une dette déjà
contractée.

Voir aussi [[documents-du-projet]], [[rapport-de-tache]].
