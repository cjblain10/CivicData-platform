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

## Repository

**Target URL:** [github.com/cblain10/CivicData-platform](https://github.com/cblain10/CivicData-platform)

If that path 404s, see **`docs/SOURCE_OF_TRUTH.md`** — pushes currently go to **`cjblain10/CivicData-platform`** until the `cblain10` repo exists or you retarget `origin`.

```bash
git remote -v
git push -u origin main
```

*Last updated: 2026-04-13*
