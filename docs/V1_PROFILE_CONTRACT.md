# V1 civic profile contract (preserve in v2)

This documents the **LocalInsights / civicdata** entry point and **entity profile shell** to re-implement in `civicdata-platform` so URLs, bookmarks, and mental models stay stable.

**Legacy codebase:** `localinsights-platform` (GitHub `cjblain10/localinsights-platform`, branch `master`).

## Canonical routes

| Route | Behavior |
|-------|----------|
| **`/entity/[id]`** | Primary **civic profile**. `id` is the stable `entity_id` string (e.g. `COUNTY_harris`, `CITY_austin`). |
| **`/entity/[id]?tab=<name>`** | Same page; **Radix tabs** driven by query param (deep-link tabs). |
| **`/county/[fips]`** | **Server redirect** to canonical entity URL built from **`counties.name`** (FIPS → name → `COUNTY_<normalized>`). Preserve query params (e.g. `tab`). |

## Entity ID construction (public URLs)

Implemented in legacy **`src/lib/entity/profile-routing.ts`**:

- **`buildCountyEntityId(countyName)`** → `COUNTY_<normalized>` (strip “County”, normalize punctuation/spacing to underscores).
- **`buildCityEntityId(cityName)`** → `CITY_<normalized>`.
- **`buildEntityProfileHref(entityId, { tab })`** → `/entity/{id}` or with `?tab=`.
- **`buildCountyProfileHref(countyName, options)`** → county entity URL.

**v2 must** reproduce the same normalization rules **or** provide a **301 map** from old IDs to new ones if you change the scheme.

## Profile UI architecture (legacy)

The page **`src/app/(platform)/(public)/entity/[id]/page.tsx`** renders a single client component:

- **`EntityProfile`** — `src/components/entity/entity-profile.tsx` (large; orchestrates data fetching, tabs, and panels).

Supporting pieces to port **incrementally** (not necessarily 1:1 file copy):

| Area | Legacy files (indicative) |
|------|---------------------------|
| Tab list & order | `entity-profile-tab-list.tsx` — Overview → Documents → … finances → records → place |
| Header / identity | `entity-profile-header.tsx`, `entity-identity-panel.tsx` |
| Loading shell | `entity-profile-skeleton.tsx` |
| Shared stat UI | `entity-profile-utils.tsx` (`StatCard`, formatters) |
| County “explore” panels | `entity-county-reference-panel.tsx`, `entity-county-spotlight-panel.tsx`, etc. |
| Heavy tabs (lazy) | `entity-money-tab`, `entity-officials-tab`, `entity-contracts-tab`, `entity-capital-projects-tab`, `entity-boundary-map` (dynamic) |

## Data wiring (v2 target)

v1 pulls from **Supabase** client helpers and **REST** `/api/*` routes. v2 should:

1. Expose **read APIs** with **pagination** and **`entity_id` / `county_fips` filters** per **`DATA_INGESTION_CONSTITUTION.md`**.
2. Keep **Tier 1** fetches **fast and cacheable**; lazy-load Tier 2/3 tab payloads.

## Metadata

Legacy layout sets **title/description** from entity in **`src/app/(platform)/(public)/entity/[id]/layout.tsx`** (with fallbacks derived from `COUNTY_` / `CITY_` id patterns).

## Checklist for v2 PR “profile parity”

- [ ] `/entity/[id]` renders with app shell (nav) consistent with product.
- [ ] `?tab=` syncs with visible tab.
- [ ] `/county/[fips]` → canonical entity URL + param preservation.
- [ ] Tier 1 strip present for **county** entities (or honest empty state).
- [ ] Coverage / freshness copy on any Tier 2+ block.

*Last updated: 2026-04-13*
