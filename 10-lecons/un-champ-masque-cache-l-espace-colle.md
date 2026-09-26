---
titre: Un champ masqué cache l'espace collé — un code se compare après avoir retiré ses bords
type: lecon
origine: FIBDA Bodybuilding — 2026-09-26
tags: [connexion, saisie, mobile, diagnostic]
---

# Un champ masqué cache l'espace collé — un code se compare après avoir retiré ses bords

**Symptôme.** « Le chef n'arrive pas à se connecter, sur tous ses appareils :
Code incorrect. » Le même code, tapé à la main par le développeur, passait.
La limite de tentatives, la désactivation de compte et l'approbation étaient
toutes hors de cause à la lecture du code.

**Cause.** Le code avait été transmis par messagerie et **collé** : un espace
ou un retour à la ligne final était venu avec. Le champ est de type mot de
passe, donc l'espace est invisible, et le serveur comparait le code à la
lettre près. La question « quel message exact ? » a suffi à écarter les autres
pistes : « Code incorrect » ne peut venir que de la comparaison.

**Règle.** Un identifiant ou un code saisi par un humain se compare **après
suppression des espaces de bord**, à la connexion comme à la création du
compte (sinon un code créé avec un espace devient impossible à saisir). Un
champ masqué offre un « Afficher » : la personne doit pouvoir voir ce qu'elle
a tapé quand le serveur refuse. Les majuscules automatiques du clavier mobile
se désactivent sur ce champ.

**Corollaire.** Avant de chercher dans le code, demander le **message exact**
affiché : chaque message n'a qu'une ou deux origines possibles.

Voir [[lire-la-donnee-avant-l-hypothese]], [[refuser-plutot-que-convertir]].
