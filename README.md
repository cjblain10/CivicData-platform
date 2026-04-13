# CivicData platform (greenfield)

Next.js application shell for a rebuilt Texas civic data product. **Rules and checklists live in `docs/platform-rebuild/`** — read [`docs/platform-rebuild/README.md`](docs/platform-rebuild/README.md) before contributing.

## Quick start

```bash
nvm use
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Documentation

| Doc | Purpose |
|-----|---------|
| [`AGENTS.md`](AGENTS.md) | AI / agent entrypoint |
| [`CLAUDE.md`](CLAUDE.md) | Stack quick reference |
| [`docs/platform-rebuild/`](docs/platform-rebuild/README.md) | Constitution: language, security, ingestion, pre-ship checklist |
| [`docs/PRODUCT_PLAN_CIVIC_PROFILE.md`](docs/PRODUCT_PLAN_CIVIC_PROFILE.md) | Tiered data strategy + profile UX (gro plan) |
| [`docs/V1_PROFILE_CONTRACT.md`](docs/V1_PROFILE_CONTRACT.md) | **Preserve:** `/entity/[id]`, tabs, `/county/[fips]` redirect (v1 contract) |

## Repository setup

1. Create an empty repo on GitHub (or your host).
2. Add remote: `git remote add origin <url>`
3. Push: `git push -u origin main`

*Last updated: 2026-04-13*
