# Pre-ship checklist

Use for **staging** and **production** releases. Check every box or record a **tracked exception** (issue link + owner + review date).

## SECURITY

- [ ] No API keys or secrets in frontend code  
  *Verify:* search repo for `sk_live`, `service_role`, `SUPABASE_SERVICE`; scan client bundles.
- [ ] Every route checks authentication (audit **all** endpoints, not just the obvious ones)  
  *Verify:* automated route inventory vs auth middleware / per-handler guards; no “forgotten” `/api/*`.
- [ ] HTTPS enforced everywhere; HTTP redirected  
  *Verify:* `curl -I http://` → 301/308 to `https://`.
- [ ] CORS locked to your domain — not wildcard  
  *Verify:* preflight from alien origin fails; prod config in repo or infra-as-code.
- [ ] Input validated and sanitized server-side  
  *Verify:* shared schema on mutating routes; tests for rejection of junk payloads.
- [ ] Rate limiting on auth and sensitive endpoints  
  *Verify:* load test or scripted burst; 429 returned.
- [ ] Passwords hashed with bcrypt or argon2  
  *Verify:* code path audit; no plaintext compare.
- [ ] Auth tokens have expiry  
  *Verify:* JWT `exp` or session TTL documented; clock skew considered.
- [ ] Sessions invalidated on logout (server-side)  
  *Verify:* post-logout token/session cannot access protected route.

## DATABASE

- [ ] Backups configured and tested (**test restore**, not just backup)  
  *Verify:* run restore drill to scratch instance; document RTO/RPO.
- [ ] Parameterized queries everywhere — no string concatenation  
  *Verify:* lint or grep for risky patterns; ORM-only counts if ORM guarantees binding.
- [ ] Separate dev and production databases  
  *Verify:* prod URL never used from local `.env` by default.
- [ ] Connection pooling configured  
  *Verify:* pool size documented; no connection storm under load.
- [ ] Migrations in version control, not manual changes  
  *Verify:* `main` migrations match prod `schema_migrations` / equivalent.
- [ ] App uses a non-root DB user  
  *Verify:* role has minimum privileges (no `SUPERUSER`, no broad `CREATE` in prod if avoidable).

## DEPLOYMENT

- [ ] All environment variables set on the production server  
  *Verify:* deploy checklist or secret manager audit.
- [ ] SSL certificate installed and valid  
  *Verify:* browser + SSL Labs or `openssl s_client`.
- [ ] Firewall configured (only 80/443 public)  
  *Verify:* infra diagram; DB not on public internet.
- [ ] Process manager running (PM2, systemd, or platform equivalent)  
  *Verify:* restart policy; health restart on failure.
- [ ] Rollback plan exists  
  *Verify:* documented steps; last rollback drill date.
- [ ] Staging test passed before production deploy  
  *Verify:* link to staging run / sign-off.

## CODE

- [ ] No `console.log` in production build  
  *Verify:* ESLint `no-console` or strip in build; structured logger only.
- [ ] Error handling on all async operations  
  *Verify:* unhandled rejection handler; route `try/catch` or framework error boundary.
- [ ] Loading and error states in UI  
  *Verify:* spot-check critical flows (auth, search, detail pages).
- [ ] Pagination on all list endpoints  
  *Verify:* API audit; max limits enforced server-side.
- [ ] `npm audit` run; critical issues resolved  
  *Verify:* CI artifact or command output attached to release.

---

*Last updated: 2026-04-13*
