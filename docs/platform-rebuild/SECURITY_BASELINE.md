# Security baseline — design-time rules

These complement [PRE_SHIP_CHECKLIST.md](./PRE_SHIP_CHECKLIST.md). Implement **before** shipping; verify in CI where possible.

## Secrets and clients

- **Never** embed API keys, service role keys, or signing secrets in frontend bundles. Use **server-only** env (`process.env` on server, Edge secrets, CI vars).
- **Separate** keys per environment (dev/staging/prod). Rotate on leave or leak.
- **Audit** `NEXT_PUBLIC_*` and any client-exposed vars quarterly — only non-sensitive config belongs there.

## Authentication and authorization

- **Every** HTTP route that mutates state or returns non-public data must enforce auth **in code**, not only behind a reverse proxy.
- **Default deny** for new routes; explicitly mark **public** routes in one module (allowlist), reviewed in PR.
- **Sessions / JWTs:** short-lived access tokens; refresh rotation optional but document threat model; **server-side invalidation** on logout (blocklist or session version bump).
- **Passwords:** **Argon2id** (preferred) or **bcrypt** with cost appropriate to hardware; never store plaintext.

## Transport and browser security

- **HTTPS** everywhere in production; HTTP → HTTPS redirect at edge.
- **HSTS** after confidence in cert setup.
- **CORS:** explicit **origin allowlist** — no `*` with credentials.

## Input and abuse

- **Validate** all inputs on the server (schema: Zod, valibot, or equivalent). Reject unknown fields where feasible.
- **Sanitize** for context: HTML output escaped; SQL only via parameters; file uploads scanned and type/size limited.
- **Rate limit** login, password reset, search, and export endpoints (IP + user id where authenticated).

## Dependencies

- **`npm audit`** (or `pnpm audit`) in CI; **block merges** on critical unless documented exception with expiry date.
- Lockfile committed; no unreviewed `latest` in production deps.

## Logging and PII

- No PII or secrets in **info-level** logs in production. Use structured logs with **redaction** for tokens and passwords.

*Last updated: 2026-04-13*
