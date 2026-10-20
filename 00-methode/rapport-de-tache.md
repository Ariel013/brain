---
titre: Rapport de tâche
aliases: [Rapport, Format de rendu]
type: methode
maj: 2026-10-20
---

# Rapport de tâche

À la fin de chaque tâche, **avant tout commit**, l'agent rend compte dans ce
format — **l'utile seulement**. Et ce n'est pas réservé au commit : **tout
retour** de l'agent, sur tous les projets, suit la même discipline — ce qui a
été fait, ce qui est remis en cause, ce qui m'attend. Une réponse courte garde
les rubriques utiles et laisse tomber les autres ; elle n'ajoute rien à côté.

```
## <la tâche en une ligne>
**Fait** : les actions effectuées et leur résultat **mesuré** — ce qui marche,
ce qui reste non vérifié (jamais « vu à l'écran » si ça ne l'a pas été).
**Sécurité** : revue du diff faite → constats (ou « aucun ») ; ou non faite
→ pourquoi (tâche sans code, par exemple). → [[revue-securite]]
**Challenge** : ce que je remets en cause dans ce qui était proposé ou reste à
faire — un risque, un meilleur ordre, une étape inutile — avec ma
recommandation.
**À toi** : les décisions à prendre et les actions manuelles, dans l'ordre.
**Commit proposé** : <message exact, non encore exécuté> (s'il y en a un).
```

Je valide le commit avant qu'il ne soit fait.

**Ce qui n'y figure pas** : la liste des fichiers touchés, des extraits de code,
le détail d'implémentation, le compte rendu brut d'un sous-agent. L'agent les
connaît et les vérifie ; il ne les remonte que s'ils changent une décision.
*(Format revu le 2026-10-18 : l'ancien, avec « Fichiers modifiés » et
« Nature », noyait l'essentiel.)*

Ni chemins de fichiers, ni commandes, ni tableaux de détail, ni récit des
étapes intermédiaires — même dans un retour hors rapport. Le test : *est-ce que
j'en ai besoin pour décider ou pour croire le résultat ?* Sinon, ça sort.
*(Élargi le 2026-10-20 : le format ne valait qu'avant commit ; les autres
retours d'une session listaient encore fichiers, commandes `git add` et
tableaux, et il fallait fouiller pour trouver l'information utile.)*

## Pourquoi ce format

- **« Fait », mesuré** : c'est ce que je dois pouvoir croire sans relire le
  code. Un résultat non mesuré n'y entre pas.
- **« Sécurité »** : une revue qui n'apparaît pas dans le rapport n'a pas eu
  lieu. La ligne oblige à dire laquelle des deux.
- **« Challenge »** : l'agent ne se contente pas d'exécuter ; il dit ce qu'il
  ferait autrement. C'est là que se rattrapent les mauvaises priorités.
- **« À toi »** : ce qui m'attend, rien d'autre — sans le chercher dans le texte.
- **« Commit proposé, non encore exécuté »** garde la main sur le message et le
  découpage. Un débordement de périmètre se signale en une phrase dans
  « Challenge », pas par une liste de fichiers.

## Ce qui doit toujours y apparaître

Un rapport signale **explicitement**, en une ligne, même si ce n'était pas le
sujet :
- un changement de schéma de base ;
- une nouvelle dépendance externe ;
- une modification touchant l'authentification, le stockage ou les données
  sensibles ;
- une convention nouvelle, à ajouter à `conventions-code.md` dans la même tâche ;
- une décision qui mériterait un ADR.

## Le pendant : quand s'arrêter et demander

L'agent tranche seul les choix techniques ordinaires — c'est ce que je veux.
Mais un choix **structurant** non encore tranché (nouvelle table, nouveau flux
de données, nouvelle dépendance lourde, changement de convention) s'arrête :

1. exposer brièvement les options et leurs compromis ;
2. une fois la décision prise, écrire l'ADR ;
3. **puis** continuer.

> Une décision prise sans être posée nulle part est une décision perdue pour la
> suite du projet. → [[ecrire-la-decision-avec-le-code]]

Voir aussi [[travailler-avec-les-agents]].
