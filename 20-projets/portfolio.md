---
titre: Portfolio
type: projet
domaine: site vitrine personnel (développeur full stack)
statut: en ligne ; dépôt sans JOURNAL.md ni CLAUDE.md (pas amorcé)
depot: ~/PROJETS/Portfolio
maj: 2026-10-25
---

# Portfolio

**Ce que c'est.** Le portfolio personnel d'Ariel Kevin SODJINOU : accueil,
à propos, compétences, expériences, projets, certifications, contact. Bilingue
FR/EN (textes dans un fichier de traductions), thème clair/sombre.

**Stack.** React + Vite + Tailwind, framer-motion. Images hébergées sur
Cloudinary. `dist` retiré du dépôt.

**À faire.** Le dépôt n'a jamais été amorcé (`/amorce-projet`) : pas de
`JOURNAL.md`, pas de `CLAUDE.md`.

## Ce que ce projet a appris au coffre

Session du 2026-10-22 (nouvelle photo, section « À propos » refaite) :

- [[arreter-un-processus-par-son-pid-pas-par-un-motif]] — seconde occurrence :
  `pgrep -f | xargs kill` se tue aussi lui-même ; un commit n'a pas eu lieu
- [[regarder-l-application-fait-partie-de-la-recette]] — une photo retirée
  laissait un trou dans la grille, invisible au build

Session du 2026-10-25 (audit impeccable, petites corrections, contraste) :

- [[un-vas-y-sur-un-audit-ne-vaut-pas-refonte]] — note créée : une refonte
  complète appliquée sur un « vas-y » a été rejetée et annulée ; le
  propriétaire tient à son design (dégradés, animations, modales)
- [[ce-que-l-ecran-promet-le-code-le-fait]] — seconde occurrence : un « ID de
  validation » qui était le nom du fichier image
- [[arreter-un-processus-par-son-pid-pas-par-un-motif]] — quatrième occurrence

Livré et poussé : faux ID retiré, interface entièrement traduite, modales
fermables à Échap, `lang` de la page synchronisé, Poppins non chargée, widget
de chat en `defer` ; puis fin des dégradés à texte blanc passée de cyan-500 à
cyan-700 (contraste 2,4 → 5,4:1). **Contrastes restants non traités**
(choix du propriétaire de ne pas toucher l'apparence) : couleur primaire sur
fond sombre 2,8:1, gris clairs secondaires ~2,5:1.

## Ce qui vaudrait d'être repris ailleurs

- Images Cloudinary servies avec `f_auto,q_auto,w_<n>` dans l'URL : la photo
  de profil passe de 1,8 Mo à 55 Ko, sans outil ni build.
