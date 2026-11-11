---
titre: Un indicatif prérempli dans un champ téléphone est écrasé par l'autoremplissage
type: lecon
origine: UKWC — 2026-11-11
tags: [formulaire, mobile, donnees]
---

# Un indicatif prérempli dans un champ téléphone est écrasé par l'autoremplissage

**Symptôme.** Formulaire d'inscription, champ WhatsApp prérempli « +229 ».
Le client teste sur son téléphone, accepte le numéro que le clavier propose :
la liste admin affiche `+61566704`. Plus d'indicatif, et un numéro qui ne
ressemble à rien (ancien format national à 8 chiffres).

**Cause.** Indicatif et numéro vivaient dans **le même champ**, en
`autocomplete="tel"`. L'autoremplissage du téléphone **remplace** la valeur du
champ, il ne la complète pas : le préremplissage disparaît sans bruit. Le
serveur, qui acceptait « 8 à 15 chiffres, + facultatif », n'avait aucune raison
de refuser.

**Règle.** Un indicatif ne se préremplit pas dans le champ du numéro :
- indicatif dans une **liste séparée** (pays par défaut sélectionné), numéro en
  `autocomplete="tel-national"` ;
- un numéro collé avec `+` ou `00` l'emporte sur la liste ;
- le serveur **normalise** les écritures courantes vers une seule forme avant
  tout dédoublonnage (`00…`, numéro local sans indicatif, ancien format du pays).

**Corollaire.** Un champ prérempli se teste **avec l'autoremplissage du vrai
téléphone**, pas seulement en tapant au clavier : c'est le chemin que prend la
majorité des visiteurs.

Voir [[un-champ-se-verifie-rempli-pas-vide]], [[normaliser-a-la-lecture]],
[[un-champ-masque-cache-l-espace-colle]].
