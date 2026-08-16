# Project Zero-Bug Release Gate

Evidence-based release checklist. UNKNOWN is never PASS.

- [ ] Requirements/device/browser/auth/API/data/integration/security/accessibility defined
- [ ] Architecture/dependencies/env/secrets reviewed
- [ ] Static audit for debug/TODO/FIXME/HACK, secrets/private keys, unsafe HTML/eval/URLs, unsafe casts, unhandled promises, races, dead code, fake success
- [ ] Install/typecheck/lint/build/routes PASS; warnings classified
- [ ] Feature normal/empty/invalid/malformed/boundary/duplicate/repeated/rapid/refresh/back/direct URL/timeout/retry/network/server failure tested
- [ ] API auth/authorization/schema/type validation; correct 4xx/5xx; safe errors; persistence before success
- [ ] Data null/undefined/nested/duplicate/concurrency/partial-write/index/query cases checked
- [ ] Security/auth, accessibility, responsive, touch/mouse, performance and network-failure checks complete
- [ ] Observability/sensitive-log review complete
- [ ] Production deployment/domain/HTTPS/env/API/assets/deep links/smoke test verified
- [ ] Runtime errors/warnings/4xx/5xx/timeouts reviewed
- [ ] Adversarial QA and regression tests complete

## Final gate
Critical bugs = 0; high-severity known bugs = 0; critical paths verified; regression tests pass; production smoke test passes; no critical UNKNOWN items.

**Build/deployment success alone never means bug-free.**