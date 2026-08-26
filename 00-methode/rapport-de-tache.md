---
titre: Rapport de tâche
aliases: [Rapport, Format de rendu]
type: methode
maj: 2026-08-26
---

# Rapport de tâche

À la fin de chaque tâche, **avant tout commit**, l'agent rend compte dans ce
format exact :

```
## Tâche : <résumé en une ligne>
### Nature : feature | fix | refactor | doc | chore
### Fichiers modifiés : <liste>
### Ce qui a changé et pourquoi : <2-4 lignes>
### Décision(s) prise(s) qui mériterait(nt) un ADR : <oui/non, laquelle>
### Commit proposé : <message exact, non encore exécuté>
```

Je valide le commit avant qu'il ne soit fait.

## Pourquoi ce format

- **« Fichiers modifiés »** rend visible un débordement de périmètre : si la
  liste ne ressemble pas à la tâche, c'est que la tâche en couvrait deux.
- **« et pourquoi »** est la seule ligne qui survivra au diff. Le *quoi* se
  relit dans le code ; le *pourquoi* se perd.
- **« mériterait un ADR »** force la question à chaque fois, au lieu de la
  laisser dépendre de la vigilance du moment.
- **« Commit proposé, non encore exécuté »** garde la main sur le message et le
  découpage.

## Ce qui doit toujours y apparaître

Un rapport signale **explicitement**, même si ce n'était pas le sujet :
- un changement de schéma de base ;
- une nouvelle dépendance externe ;
- une modification touchant l'authentification, le stockage ou les données
  sensibles ;
- une convention nouvelle, à ajouter à `conventions-code.md` dans la même tâche.

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
