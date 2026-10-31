---
titre: CV interactif
type: projet
domaine: CV web personnel (candidatures d'alternance)
statut: en ligne depuis le 2026-10-25 (iamariel.vercel.app)
depot: ~/PROJETS/cv-interactif
maj: 2026-10-25
---

# CV interactif

**Ce que c'est.** Le CV web de Kevin, envoyé par lien dans ses candidatures
d'alternance fullstack et IA. Une île en 3D qu'on explore avec un
personnage, avec joystick sur mobile, sons, une flèche qui guide vers le
contact, et un mode terminal pour le public tech. Français et anglais.
Chat IA étudié puis abandonné (clé payante). La page 2D, puis le mur LED,
ont été rejetés par Kevin avant l'île (« je ne vois qu'un portfolio »). Remplace `Curriculum`, dérivé d'un modèle open-source, dont le
contenu avait dérivé du CV maître.

**Stack.** Next.js + React Three Fiber sur Vercel. Contenu : copie
publique du CV maître d'[[optimisation-cv]], sans base de données.

## Ce que ce projet a appris au coffre

- [[un-cache-de-build-restaure-peut-servir-l-ancienne-feuille-de-style]]
- [[un-champ-qui-ne-s-envoie-qu-avec-entree-est-bloque-sur-telephone]]
- [[un-ecran-mobile-se-teste-a-la-hauteur-visible-pas-seulement-a-la-largeur]]
- Occurrences ajoutées à [[une-fonction-serverless-s-envoie-regroupee-et-se-verifie-au-curl]]
  (Vercel sans framework : pages en 404), [[nommer-la-copie-visee]] (fusion
  dans la copie d'une autre session) et
  [[arreter-un-processus-par-son-pid-pas-par-un-motif]].

## Ce qui vaudrait d'être repris ailleurs

- Une seule source de faits partagée entre deux projets, sans dépendance au
  build : une copie publique générée par script, avec l'empreinte de sa source.
- Pour un CV ou un portfolio, montrer tôt une version jouable : deux
  directions validées sur le papier (page 2D, mur LED) ont été rejetées à
  l'écran.
