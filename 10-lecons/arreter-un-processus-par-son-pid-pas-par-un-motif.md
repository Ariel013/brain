---
titre: Un processus s'arrête par son PID, pas par un motif qui figure dans la commande
type: lecon
origine: Optimisation CV — 2026-10-20
tags: [shell, agents]
---

# Un processus s'arrête par son PID, pas par un motif qui figure dans la commande

**Symptôme.** Pour arrêter un serveur de développement, l'agent lançait
`pkill -f "next dev"; <suite du travail>` dans une même commande. La suite
(mise à jour du journal et de l'ADR) n'a jamais eu lieu : code de sortie 144,
sans message. Le travail a été cru fait jusqu'à ce qu'un `grep` le démente.

**Cause.** `pkill -f` compare le motif à la ligne de commande complète de
**tous** les processus — y compris le shell qui exécute la commande, puisque
le motif y figure. Il s'est tué lui-même.

**Règle.** Trouver le PID (`pgrep -f …` dans une commande à part, vérifier par
`ps -o pid,args`), puis `kill <PID>`. Et vérifier qu'une étape a eu lieu par
son effet (le fichier modifié), pas par l'absence d'erreur.

**Seconde occurrence — Portfolio, 2026-10-22.** Même chute, deux fois dans la
même session, malgré la note : `pkill -f "vite preview --port 4799"; rm …`
(le nettoyage n'a pas eu lieu), puis le « correctif »
`pgrep -f "vite preview --port 4799" | xargs -r kill; git commit …` — `pgrep -f`
voit lui aussi le shell qui porte le motif. Code 144, **le commit n'a pas eu
lieu** ; seul un `git log` relu juste après l'a montré.

**Corollaire.** Remplacer `pkill` par `pgrep | xargs kill` ne change rien tant
que le motif est dans la ligne. Le plus sûr : garder le PID au lancement
(`cmd & echo $!`), ou arrêter dans une commande qui ne fait **que** ça, puis
vérifier l'effet (`ss -ltnp | grep <port>`).

Voir [[une-etape-de-recette-nommee-n-est-pas-une-etape-lancee]], [[verifier-chaque-commit-du-decoupage]].
