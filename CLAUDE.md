# CLAUDE.md — CivicData platform (greenfield)

Texas civic intelligence — rebuilt with strict security, ingestion, and shipping rules.

## Read first

- **`docs/platform-rebuild/README.md`** — mandatory doc order for humans and agents.
- **`docs/platform-rebuild/DATA_INGESTION_CONSTITUTION.md`** before any pipeline or schema write.

## Quick start

```bash
nvm use   # see .nvmrc
npm ci
npm run dev
npm run lint
npm run build
```

## Stack (initial)

| Layer | Tech |
|-------|------|
| Framework | Next.js (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS v4 |

Database, auth, and deploy choices are **TBD** — document them here when chosen, and align with **`docs/platform-rebuild/ARCHITECTURE_PRINCIPLES.md`**.

## Git

- Default branch: **`main`** until you rename.
- No secrets in commits; `.env*` is gitignored.

*Last updated: 2026-04-13*
