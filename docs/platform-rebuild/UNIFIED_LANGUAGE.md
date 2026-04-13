# Unified language — civic data platform

Public-facing and internal naming should reinforce **transparency and journalism**, not law enforcement or enterprise surveillance.

## Product framing

| Avoid | Prefer |
|-------|--------|
| Investigation | Data story, analysis, narrative |
| Bloomberg Terminal (metaphor) | Civic intelligence platform |
| Investigate | Research, explore, analyze |
| Case (for user work) | Story, project, saved view |
| Surveillance, monitoring people | Monitoring *datasets*, freshness, pipeline health |

## User-facing errors

- Be **specific enough to act** (“Request timed out; try again”) without leaking internals (no stack traces, no SQL, no bucket names).
- Use **neutral institutional tone** — not alarmist, not cute.

## API and data vocabulary

- **Entity** — canonical jurisdiction or actor with a stable ID (county, city, district, person/org in money graph when applicable).
- **Provenance** — source system, retrieval time, and method (API, scrape, file import).
- **Freshness** — last successful ingest or source `as_of` date; distinguish **pipeline run time** from **data vintage**.
- **Public record** — data lawfully published by government or derived from it; do not imply private-sector “ownership.”

## Tiers (product)

Use **Tier 1–4** only with definitions tied to **coverage and honesty** (e.g. statewide county comparability), not marketing. If tiers are used in UI, show **coverage %** or **scope labels** where data is partial.

## Texas / civic context

- Prefer **FIPS `48xxx`** for Texas counties in storage and APIs once normalized; document any legacy key in field comments, not only in chat.

*Last updated: 2026-04-13*
