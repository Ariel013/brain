---
titre: Publier un détail en tout ou rien, et le tester en lecteur qui connaît la règle
type: lecon
origine: Synoé — 2026-10-12
tags: [secret, statistiques, masquage, tests, relecture]
---

# Publier un détail en tout ou rien, et le tester en lecteur qui connaît la règle

**Symptôme.** Masquer les petits effectifs (1 ou 2) d'un rapport remis à un
employeur. Chaque passe de relecture sécurité trouvait une nouvelle façon de
retrouver un compte masqué, juste après la correction de la précédente :
- par **soustraction** avec un total publié ailleurs (nombre de visites) ;
- par l'**effectif imprimé** (« moins de 3 » dans une entreprise d'un salarié) ;
- par une **autre section** du même document (une ligne « visites pour
  accident du travail : 1 » au-dessus d'accidents « moins de 3 ») ;
- par les **cas particuliers ajoutés pour colmater** : « regrouper si une seule
  conclusion » trahissait l'unanimité ; « fondre avec le plus petit type »
  disait que les types visibles étaient plus grands ; « absorber des types
  jusqu'à atteindre 3 » disait, par le nombre absorbé, que les premiers étaient
  petits.

**Cause.** Quand le total d'une ventilation se lit ailleurs, chaque décision de
masquage est **elle-même une information**. Un masquage ligne à ligne, enrichi
de cas particuliers, se recoupe toujours ; la relecture humaine ne trouve les
fuites qu'une à une.

**Règle.**
1. Publier le détail en **tout ou rien**, sur des conditions simples (au moins
   deux lignes, chacune ≥ seuil, le reste ≥ seuil…), sinon une seule ligne
   regroupée. Un choix (avec qui fusionner) ne dépend jamais des nombres.
2. Le tester en **lecteur qui connaît la règle** : énumérer tous les mondes
   possibles, calculer ce que chacun publie, et vérifier que chaque valeur
   cachée garde au moins deux valeurs possibles parmi les mondes qui publient
   la même chose — y compris le fait même de regrouper.

C'est ce test, pas la relecture, qui a arrêté les fuites : il a refusé deux
consignes de l'orchestrateur qui fuyaient.

**Corollaire.** Le masquage se fait dans le **calcul**, pas à l'affichage, pour
qu'un instantané signé ou un export en profite ; un compte ne s'imprime jamais
brut.

Voir aussi [[des-tests-verts-ne-remplacent-pas-une-relecture-adverse]],
[[le-calcul-sort-de-l-ecran]], [[un-garde-absolu-n-a-pas-d-exception-il-a-une-autre-porte]].
