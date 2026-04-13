# Platform rebuild — canonical docs (read before code)

Use this folder as the **constitution** for the new repository. Copy it wholesale into the new repo root (or keep as submodule). **No feature work** until the relevant doc is read.

## Mandatory reading order

| Order | Document | Who |
|-------|----------|-----|
| 1 | [UNIFIED_LANGUAGE.md](./UNIFIED_LANGUAGE.md) | Everyone |
| 2 | [SECURITY_BASELINE.md](./SECURITY_BASELINE.md) + [PRE_SHIP_CHECKLIST.md](./PRE_SHIP_CHECKLIST.md) | Everyone |
| 3 | [DATA_INGESTION_CONSTITUTION.md](./DATA_INGESTION_CONSTITUTION.md) | Anyone touching pipelines, migrations, or Supabase writes |
| 4 | [ARCHITECTURE_PRINCIPLES.md](./ARCHITECTURE_PRINCIPLES.md) | Anyone designing APIs, auth, or deploy |

## Rules of engagement

- **Single source of truth:** These docs override ad-hoc chat instructions when they conflict.
- **Change control:** Amending the constitution requires a PR that updates this README’s “Last updated” line and, if needed, `AGENTS.md` at repo root.
- **Agents / AI:** Repo root `AGENTS.md` must list this reading order; automation should fail or warn if `DATA_INGESTION_CONSTITUTION.md` is not acknowledged for ingestion tasks.

*Last updated: 2026-04-13*
