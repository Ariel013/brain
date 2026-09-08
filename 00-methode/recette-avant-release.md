---
titre: Recette avant release
aliases: [Recette, Checklist release]
type: methode
maj: 2026-09-08
---

# Recette avant release

> Des tests verts ne prouvent que ce qu'ils exercent. Trois écrans blancs sont
> déjà passés à travers 480 tests, un build vert et un typecheck vert.
>
> Et une étape **nommée** n'est pas une étape **lancée** : un lot déclaré
> « typecheck vert » ne compilait pas, les deux scripts de build appelant
> `tsc --noCheck` → [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]].

## L'ordre

0. **Lire les scripts de recette du dépôt**, une fois par projet : vérifier
   qu'aucun drapeau n'y désarme le contrôle que le nom promet (`--noCheck`,
   `--no-verify`, `--passWithNoTests`, `|| true`, `continue-on-error`).
1. **Typecheck** — sur chaque niveau de la remontée, pas seulement sur `dev`.
   Lancé **nommément**, son code de sortie lu : un build vert ne le remplace pas.
2. **Tests** — rejoués **après chaque fusion**, pas une fois au début.
3. **Build** — un build qui passe en local ne prouve pas que le bundle servi est
   le bon (voir §5).
4. **Passe visuelle** — ouvrir **chaque écran touché**. Automatisable sans rien
   installer : un mode local forcé par un `.env` gitignoré, un second serveur sur
   un autre port pour ne pas déranger celui du dev, puis une capture par route en
   navigateur sans interface. Aucun identifiant, aucune donnée réelle — mais un
   écran mort se voit immédiatement.
   → [[regarder-l-application-fait-partie-de-la-recette]]
5. **Balayer les largeurs** — pas seulement 1440 px. 999, 780, 560, 420. Deux
   défauts de mise en page en deux jours n'ont été vus que comme ça. Et **mesurer
   plutôt que croire l'image** : demander à la page ce qu'elle voit
   (`innerWidth`, `scrollWidth`) → [[mesurer-l-outil-avant-de-conclure]].
6. **Vérifier le déploiement par ce qui est servi**, pas par le fait d'avoir
   poussé : le bundle servi est-il celui du build de `main` ? les routes internes
   répondent-elles (pas de 404 au rafraîchissement) ? la nouveauté est-elle
   réellement présente dans le chunk téléchargé ?

## Avant de taguer

- Le périmètre de la release est **décidé et énoncé** ; le travail s'arrête là
  → [[une-release-se-coupe-sur-un-perimetre]].
- `git diff main dev` **vide**.
- Le tag pointe bien le commit voulu — vérifié par `rev-parse`, pas supposé
  → [[nommer-la-copie-visee]].
- Sauvegarde des données réelles **vérifiée** (déchiffrée, lignes comptées) :
  la taille d'un fichier ne prouve rien.

## Ce qu'une recette ne voit pas

Ces défauts ne se prennent qu'en y pensant explicitement :

- **Une donnée qui vit à l'écran mais n'est jamais écrite**
  → [[verifier-le-chemin-d-ecriture]].
- **Un écran qui promet ce que le code ne fait pas**
  → [[ce-que-l-ecran-promet-le-code-le-fait]].
- **Une fonctionnalité qui marche mais que rien n'annonce**
  → [[une-fonctionnalite-invisible-est-absente]].
- **Un test de garde qui passe pour de mauvaises raisons**
  → [[casser-le-test-expres]].
- **Une consigne remise à l'utilisateur qui décrit l'intention et non l'écran**
  → [[une-consigne-executable-se-redige-contre-le-code]].
