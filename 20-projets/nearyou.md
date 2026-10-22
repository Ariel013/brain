---
titre: NearYou (GéoService)
type: projet
domaine: annuaire géolocalisé de prestataires de services locaux (Bénin, Côte d'Ivoire)
statut: en ligne ; dépôt sans JOURNAL.md (pas amorcé)
depot: ~/PROJETS/NearYou
maj: 2026-10-22
---

# NearYou (GéoService)

**Ce que c'est.** Fiches de prestataires (menuisiers, plombiers…) créées par la
communauté, revendiquées par le prestataire via un bot WhatsApp ; recherche par
distance sur carte Leaflet/OpenStreetMap.

**Stack.** Next.js 16 sur Vercel, Supabase (PostgreSQL + PostGIS) sur le plan
gratuit, bot WhatsApp sur Railway (ne touche pas la base).

**À faire.** Le dépôt n'a jamais été amorcé (`/amorce-projet`) : `CLAUDE.md`
présent, mais pas de `JOURNAL.md` ni de `docs/decisions/`.

## Ce que ce projet a appris au coffre

Session du 2026-10-22 (base en pause, migration vers un nouveau compte Supabase) :

- [[un-maintien-en-vie-ne-depend-pas-de-l-activite-qu-il-remplace]] — le cron
  GitHub s'est éteint avec l'inactivité du dépôt ; remplacé par un cron Vercel
- [[arreter-un-processus-par-son-pid-pas-par-un-motif]] — troisième occurrence

## Ce qui vaudrait d'être repris ailleurs

- **Migrer une base Supabase d'un compte à l'autre** : copier le schéma `public`
  **réel** (pas rejouer les migrations, qui peuvent avoir divergé) avec un
  `pg_dump` de la **même version majeure** que le serveur (ici 17, présent dans
  `/usr/lib/postgresql/17/bin`) ; recréer d'abord les extensions dans le même
  schéma (PostGIS était dans `public`) ; écarter les objets fournis par la
  plateforme (`rls_auto_enable`, données de `spatial_ref_sys`). Puis comparer
  ancien et nouveau : lignes par table, politiques RLS, activation RLS,
  fonctions, triggers, index, droits `anon`/`authenticated`/`service_role` —
  et un appel RPC sous `set role anon`. Prouver enfin la bascule par une
  écriture faite depuis le site en production, relue dans la nouvelle base.
- Les nouveaux projets Supabase fournissent des clés `sb_publishable_…` /
  `sb_secret_…` : elles remplacent anon / service_role sans changer le code.
