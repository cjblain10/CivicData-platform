# Product plan — civic profile & platform rebuild

Synthesized from the **gro** strategy brief (tiered data reality + premier civic intelligence positioning) and aligned with **`docs/platform-rebuild/UNIFIED_LANGUAGE.md`** (journalism / transparency framing — gate **features**, not **public records**).

## Strategic spine

**Five statewide-comparable county datasets (254/254 Texas counties)** are the **skeleton** for the flagship experience:

| Dataset | Role on profile |
|---------|-----------------|
| `oca_court_stats` | Courts / filings context |
| `tcjs_population` (+ turnover where used) | Jail / capacity story |
| `social_services_enrollment` | Social safety-net signal |
| `census_acs_metrics` (county grain only) | Demographics / economic comparables |
| `counties` + `entities` | Identity, resolution, cross-links |

Everything else is **connective tissue**: show **with coverage badges**, **freshness**, and **methodology** when partial or entity-scoped.

## Tier placement (product)

- **Tier 1 — Report card strip** — Only metrics that are honestly statewide at county grain (table above). No implied completeness.
- **Tier 2 — Conditional modules** — Census COG finance (~66 counties deep), special districts / ISDs / cities (linkage incomplete), tax and bond signals, EMMA/ACFR-derived fiscal rows where `entity_id` exists, federal audits/grants APIs, labor, etc. **Label partial coverage.**
- **Tier 3 — Platform modules** — Money graph, HCDC, Odyssey, permits, 311, TEA PEIMS at ISD grain, elections volume, water, agendas, niche tables. **Never default “official overview” for all counties.**
- **Tier 4 — Do not ship as universal** — Empty pipelines (`contracts_state`, `fiscal_metrics`, BLS/OSHA if empty), broken keys (`federal_awards_county_summary`), **`entity_boundaries` until FIPS arrays are fixed** (block **map-as-truth** launches).

## Page anatomy (target UX)

1. **Entry** — Same contract as v1: canonical **`/entity/[entityId]`**; optional **`?tab=`**; legacy **`/county/[fips]`** redirects into entity URL (see **`docs/V1_PROFILE_CONTRACT.md`**).
2. **Above the fold** — County/jurisdiction identity + **Tier 1 strip** (compact comparables + links to topic pages).
3. **Tabs** — **Overview → Documents (when data) → finances → records → place** (county/city), with **progressive disclosure**; sparse tabs show empty states with **why** and **coverage %** where relevant.
4. **Platform** — Deeper tools (exports, saved views, alerts, workspace) sit **outside** the “public record card” promise; gate **workflow**, not **raw facts**.

## Gating model

| Always public | Behind account / tier |
|---------------|------------------------|
| Core public records & Tier 1 strip | Bulk export, API keys, team workspace |
| Source links & provenance | Advanced graph depth, saved investigations |
| Methodology & freshness | (Product-specific — document per feature) |

**Rule:** If the government published it as open data, the **default** is **discoverable** at appropriate depth; **paid** layers add **convenience, scale, and collaboration**, not **hiding the record**.

## Rebuild sequence (phased)

Phases map to the gro brief; adjust calendar to team size.

1. **Core 254** — Auth, entity resolution, county profile shell, APIs for OCA / TCJS / social / ACS / entities only.
2. **Tier 2 modules** — Conditional sections + coverage UI; start EMMA/ACFR **read** paths only where keyed.
3. **Tier 3 platform** — Money, courts verticals, permits, education, etc., each with **scope labels**.
4. **Maps / boundaries** — Only after **`entity_boundaries`** (or successor) joins are trustworthy.
5. **Business layer** — Billing, orgs, API product, rate limits (see **`PRE_SHIP_CHECKLIST.md`**).

## Pipeline priorities (highest leverage)

1. **County FIPS hygiene** — `school_districts`, `cities`, `special_districts` NULL/bad rows (unlocks honest Tier 2).
2. **EMMA / `govt_documents` parse backlog** — Storage exists; **parsing + `entity_id`** unlocks Tier 2 fiscal story without over-claiming.
3. **Retire or quarantine** Tier 4 tables in UI until imports or keys are fixed.

## Design system (trust)

- **Coverage badge** — “Data for X of 254 counties” or entity-scoped equivalent.
- **Freshness** — `as_of` / last ingest, not just “updated today.”
- **Methodology** — Tooltip or drawer: source, grain, known gaps.

## Relationship to v1

**Preserve the v1 civic profile contract** (URLs, tab model, redirect behavior) while re-implementing stack, auth, and APIs in this repo. See **`docs/V1_PROFILE_CONTRACT.md`** for the concrete porting checklist.

*Last updated: 2026-04-13*
