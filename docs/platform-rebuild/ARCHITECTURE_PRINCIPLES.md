# Architecture principles — greenfield

Stack-agnostic defaults; replace “Next.js / Supabase” with your chosen equivalents but **keep the invariants**.

## Layers

1. **Edge / CDN** — TLS termination, redirects, static assets, WAF if used.
2. **Application** — Request handling, authz, validation, orchestration.
3. **Data** — PostgreSQL (or equivalent) with **least-privilege** DB user for app; migrations versioned.
4. **Object storage** — PDFs and large blobs; **never** expose bucket credentials to clients; signed URLs or server proxy.

## API design

- **REST or RPC** with consistent error shape (`code`, `message`, optional `details` for dev-only).
- **Pagination** mandatory for lists; document max page size.
- **Versioning** (`/api/v1/...`) before breaking changes.
- **Idempotency** for POST that create resources where retries matter (`Idempotency-Key` header optional).

## Configuration

- **12-factor:** config in environment; no secrets in repo.
- **Feature flags** for risky paths; default off in prod until checklist green.

## Observability

- Health check that verifies **DB connectivity** (not just process up).
- Structured logs + request id propagation.
- Alerts on error rate and auth failure spikes.

## Deployment

- **Staging** mirrors prod topology minimally (same auth model, real TLS).
- **Rollback:** previous image/release tagged; database rollback via **forward-only migrations** + feature flags (avoid `DOWN` migrations in prod unless practiced).

*Last updated: 2026-04-13*
