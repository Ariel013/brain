---
titre: Modèle — point d'avancement
type: modele
cible: docs/points-avancement.md
maj: 2026-08-26
---

# Modèle — point d'avancement

> Le seul document écrit **pour l'utilisateur final**, pas pour un développeur.
> Un point à la fin de chaque module. Il répond à une question que ne couvre
> aucun autre doc : **qu'est-ce qui change pour sa pratique ?**

```markdown
## AAAA-MM-JJ — <Titre dans les mots de l'utilisateur>

**Module** : <ce qui a été livré, et dans quelle version.>

### 1. Ce qui change pour vous

<L'effet concret sur le travail quotidien. Des phrases, pas des noms de
fonctionnalités. On décrit le geste, pas l'écran.>

> ⚠️ <La limite honnête : ce que la nouveauté ne peut pas faire, et pourquoi.>

### 2. Ce qui était cassé

<Nommé sans détour, **y compris ce que personne n'avait vu**. Un défaut caché
avoué crée plus de confiance qu'un défaut tu.>

### 3. Ce qui reste ouvert

<Ce qui n'est pas fait, et pourquoi ça ne l'est pas.>

### 4. Ce qu'on attend de vous

**Marche à suivre — <ce qu'on vérifie>**

1. <Étape qui **fabrique elle-même** l'état préalable dont elle a besoin.>
2. <Étape avec le résultat attendu écrit à côté.>
3. <…>

<Ce qu'il faut nous dire si le résultat diffère.>
```

**Les deux pièges.**
- Une marche à suivre qui **suppose** un état préalable est intestable : son
  échec sera lu comme un défaut du logiciel
  → [[une-fonctionnalite-invisible-est-absente]].
- Écrire « ce qui était cassé » sans détour est ce qui distingue un point
  d'avancement d'une communication commerciale.

Voir [[documents-du-projet]].
