---
titre: L'inscription à une offre « gratuite » se fait avant d'écrire l'ADR
type: lecon
origine: FIBDA Bodybuilding — 2026-09-23 · Optimisation CV — 2026-10-20
tags: [hebergement, adr, verification, delai]
---

# L'inscription à une offre « gratuite » se fait avant d'écrire l'ADR

**Symptôme.** À J-3 d'une compétition, l'ADR d'hébergement est écrit, la
procédure de déploiement rédigée sur une VM « Always Free », les actions du PO
listées. Le PO s'inscrit : le fournisseur exige un paiement. Une heure de
rédaction à jeter, et la décision à reprendre le soir même — deux fois, puisque
le second choix (essai sans carte) a lui aussi été écarté par le PO avant
d'être exploité.

**Cause.** Les offres gratuites d'hébergement changent de mois en mois (palier
fermé aux nouveaux comptes, quota divisé par deux sans annonce, carte exigée
« pour vérification »). Une recherche web du jour ne dit pas ce que verra
**ce** compte, dans **ce** pays, avec **cette** carte. L'ADR a été fondé sur une
lecture, pas sur une ressource existante.

**Règle.** Un ADR d'hébergement ne s'écrit qu'une fois **la ressource créée et
atteinte** (compte ouvert, machine ou base provisionnée, un `curl` qui répond).
Tant que ce n'est pas fait, la décision reste « proposée » et la procédure ne
s'écrit pas. Corollaire : quand le délai est court, on dit au PO que
« gratuit et fiable » n'existe peut-être pas, et qu'un petit montant achète la
certitude — avant de dépenser des heures à contourner.

**Seconde occurrence — une autorisation « sans accord d'administrateur »
(Optimisation CV, 2026-10-20).** Pour envoyer depuis une adresse d'école
(Microsoft 365), Azure affichait l'autorisation `Mail.Send` avec « consentement
de l'administrateur requis : non ». Le code et un amendement d'ADR ont été écrits
sur cette foi. À la première connexion réelle : « Approbation requise » — l'école
avait fermé tout consentement des utilisateurs. La colonne d'Azure décrit
l'autorisation, pas la règle de l'annuaire. Même règle, étendue : **une
possibilité qui dépend d'un tiers se dit « possible » seulement après l'essai
réel**, et l'ADR garde une voie de repli disponible tout de suite (ici : Gmail,
et l'envoi à la main).

Voir [[ecrire-la-decision-avec-le-code]], [[mesurer-l-outil-avant-de-conclure]].
