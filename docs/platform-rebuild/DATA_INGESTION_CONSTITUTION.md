# Data ingestion constitution — hard rules

Violations create **invisible data** (rows in the database that never surface in the API or UI) or **trust failures** (wrong grain, no provenance).

## Non-negotiables

1. **No write-only tables** — If a script writes to a table, there must be a **read path**: documented API route (or materialized view consumed by one) **and** a planned or existing UI surface, **or** the table is explicitly scoped as internal-only in this doc and **must not** hold user-facing facts.
2. **Stable keys** — Every row that appears in the product must be joinable to **county FIPS (when geographic)**, **`entity_id` (when entity-scoped)**, or another documented resolver. No orphan facts.
3. **Provenance on every ingest** — Populate at minimum: `source` / `source_id` (or equivalent), **`retrieved_at` or `ingested_at`**, and **`source_url` or API identifier** where applicable.
4. **Parameterized queries only** — No string-concatenated SQL in any language. Use driver parameters / query builders that bind values.
5. **Idempotent upserts** — Pipelines must be safe to re-run: define **natural keys** or use **dedupe keys**; document conflict behavior (`ON CONFLICT`, merge rules).
6. **Pagination on list APIs** — Any endpoint that returns lists of ingested rows supports **cursor or offset/limit** with caps; no unbounded `SELECT *` for clients.
7. **Schema in version control** — All DDL via **numbered migrations** in git; **no** manual prod edits without a matching migration file.
8. **Staging before prod** — New tables/columns land in **dev/staging** first; smoke test read API + one UI consumer before prod.
9. **Secrets** — Ingestion uses **server-side env** or **CI secrets** only; never commit keys; never pass secrets to the browser.
10. **Rate limits and robots** — Respect source ToS; backoff on 429/5xx; log failures to **`etl_logs` / `ingestion_runs`** (or successor table).

## “Invisible data” prevention checklist (per new dataset)

- [ ] Migration defines table + indexes for lookup patterns.
- [ ] Read API documents filters: `entity_id`, `county_fips`, date range, pagination.
- [ ] Row-level security / policies aligned with **public vs authenticated** product rules.
- [ ] `docs/` matrix row updated: **table → API → UI → entity linkage**.
- [ ] Freshness surfaced in **pipeline status** or **metric registry**.

## Raw public records

**Principle:** Lawfully public records stay **public** in the product unless a separate legal/policy review says otherwise. Paywalls and “teaser” gating apply to **derivatives and tools**, not to the underlying record where policy requires openness.

*Last updated: 2026-04-13*
