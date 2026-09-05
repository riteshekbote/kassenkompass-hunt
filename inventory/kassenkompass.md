# KassenKompass GmbH inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
api.kassenkompass.de
kassenkompass.de
www.kassenkompass.de

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 3 hosts | **Live HTTP:** 0

| Host | Status | Server/Tech |
|---|---|---|

## 2026-09-02 21:45:31 UTC

## 2026-09-02 23:58:49 UTC

## 2026-09-03 04:13:45 UTC

## 2026-09-03 09:04:36 UTC

## 2026-09-03 13:34:54 UTC

## 2026-09-03 17:32:49 UTC
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
- NEW www.kassenkompass.de — mirrors kassenkompass.de
- CHANGED Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)

## 2026-09-03 20:02:53 UTC
- NEW `/sync/` returns HTTP 200 + auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401, not 200)
- NEW `/health/` confirmed unprotected, returns `{"status":"ok"}` + PHP version disclosure (`x-powered-by: PHP/8.4.3`)
- NEW All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
- NEW Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
- NEW `/insurance_info/{kk_id}` returns proper RFC 9457 401 error (unlike `/sync/`), confirming inconsistent error handling across endpoints
- NEW No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
- CHANGED API catalog confirmed 15 endpoints; `/health/` is only fully unprotected endpoint

## 2026-09-03 22:32:22 UTC
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
- NEW www.kassenkompass.de — mirrors kassenkompass.de
- CHANGED Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
- NEW `/sync/` returns HTTP 200 + auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401, not 200)
- NEW `/health/` confirmed unprotected, returns `{"status":"ok"}` + PHP version disclosure (`x-powered-by: PHP/8.4.3`)
- NEW All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
- NEW Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
- NEW `/insurance_info/{kk_id}` returns proper RFC 9457 401 error (unlike `/sync/`), confirming inconsistent error handling across endpoints
- NEW No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
- CHANGED API catalog confirmed 15 endpoints; `/health/` is only fully unprotected endpoint
- NEW `/sync/` with ANY supplied X-API-Secret value returns distinct body `"Ungültiger X-API-Secret"` (invalid) vs `"fehlt"` (missing) — gate genuinely enforced, not bypassable by header presence
- NEW Partner password-reset magic `KKX3382745` does NOT authenticate as API secret (returns "Ungültiger") — no cross-asset credential reuse
- NEW No access-control-allow-origin reflection for arbitrary Origin on api — CORS misconfig REJECTED
- NEW `/post/` also requires X-API-Secret; GET/OPTIONS reveal no bypass
- CHANGED All API data endpoints remain auth-gated; no egress to AUTH_HELPED hypotheses this session
- NEW /sync/ returns HTTP 200 with auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401)
- NEW /health/ unprotected, discloses PHP version via `x-powered-by: PHP/8.4.3`
- NEW All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
- NEW Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
- NEW `/insurance_info/{kk_id}` returns proper RFC 9457 401 error — inconsistent error handling vs `/sync/`
- NEW No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
- CHANGED API catalog confirmed 15 endpoints; `/health/` only fully unprotected endpoint

## 2026-09-04 00:35:39 UTC
- NEW `/sync/` with any X-API-Secret value returns distinct error `"Ungültiger X-API-Secret"` (invalid) vs `"fehlt"` (missing) — auth gate genuinely enforced, not bypassable by header presence alone
- NEW Partner password-reset magic `KKX3382745` does NOT authenticate as API secret — no cross-asset credential reuse
- NEW No `access-control-allow-origin` reflection for arbitrary Origin on api — CORS misconfig REJECTED
- NEW `/post/` also requires X-API-Secret; GET/OPTIONS reveal no bypass
- CHANGED All API data endpoints remain auth-gated; no egress to AUTH_HELPED hypotheses this session
- CHANGED Probe confirmation: `/user/1`, `/delete/1`, `/user/100`, `/insurance_info/1`, `/settlement_report/9999/13` all return HTTP 401 without auth

## 2026-09-04 05:10:14 UTC
- NEW Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — suggests two separate auth middleware paths
- NEW `/cat_detail/` catalog advertises GET but actually requires POST (returns 405 for GET) — catalog discrepancy
- CHANGED `/settlement_report/9999/13` confirmed: 401 (no auth) / 403 (invalid auth) — proper RFC 9457 format, consistent with majority of endpoints
- CHANGED `/sync/` remains sole endpoint returning HTTP 200 with auth error body (known MISCONFIG)

## 2026-09-04 09:51:41 UTC
- NEW Two distinct 403 error messages across API endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — two separate auth middleware stacks
- NEW `/cat_detail/` catalog says GET but returns 405, requires POST — catalog method-spec inaccuracy
- CHANGED Settlement_report endpoint confirmed: proper 401/403 RFC 9457 format — no misconfiguration here
- CHANGED `/sync/` remains sole endpoint returning HTTP 200 + auth error body

## 2026-09-04 14:21:08 UTC

## 2026-09-04 17:44:02 UTC

## 2026-09-04 20:04:27 UTC

## 2026-09-04 22:21:25 UTC

## 2026-09-05 00:22:25 UTC
- NEW api.kassenkompass.de: v2 route sweep (24 names incl. all 14 v1 endpoints + user/partner/products/config/status/search/offers/rates) → every name router-404 except `insurance_info`; v2 surface confirme
- NEW api.kassenkompass.de: exact auth-wording map nailed — v1 majority AND v2 share middleware A (`Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`); only `/user/{ext_id}` uses middlewa
- NEW api.kassenkompass.de: X-API-Secret is the SOLE auth channel on every path — `Authorization: Bearer`, `X-API-Key`, `X-Api-Token`, `api_key=` query all → 401 "erforderlich" on middleware A and B; no alt
- NEW api.kassenkompass.de: magic `KKX3382745` (sha256 bc2cb4e9…) and `X8372` (sha256 a4197524…) rejected (403) on ALL three auth paths incl. previously-untested middleware-B and v2 — CRED_REUSE closed comp
- NEW kassenkompass.de: funnel (`bonusrechner.php`) server-side mirrors raw pass-params into 1-year cookies with NO validation — `lizenz`→`afilcode`, `jid`→`customerid`, `agn`|`connectionnumber`→`agenturnum
- NEW kassenkompass.de: inventory expansion — `awv.kassenkompass.de` (self-hosted GTM proxy, nginx, `/gtm.js?id=GTM-TT4LBVMW`, root=400 noindex) and `load.awv.kassenkompass.de` (Cloudflare-challenged loader
- NEW kassenkompass.de: funnel entry map (`param_passthrough.js` v=web1.0.0, commented "kk-web-draft" refactor 2026-08-30) — `bonusrechner*.php` + `termin.php` are the only app entry points; server-side "Co

## 2026-09-05 04:47:18 UTC
- NEW api.kassenkompass.de: v2 router sweep complete — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed
- NEW api.kassenkompass.de: Auth middleware map finalized — v1 majority + v2 share middleware A (`Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`); only `/user/{ext_id}` uses middleware
- NEW api.kassenkompass.de: X-API-Secret confirmed SOLE auth channel — `Authorization: Bearer`, `X-API-Key`, `X-Api-Token`, `api_key=` query all return 401 "erforderlich" on middleware A and B; no alternate
- NEW api.kassenkompass.de: Magic `KKX3382745` (sha256 bc2cb4e9…) and `X8372` (sha256 a4197524…) rejected (403) on ALL three auth paths including middleware-B and v2 — CRED_REUSE closed completely
- NEW kassenkompass.de: Funnel (`bonusrechner.php`) server-side mirrors raw pass-params into 1-year cookies with NO validation — alias map `jid|customerid→customerid`, `agn|connectionnumber→agenturnummer`, 
- NEW kassenkompass.de: Two new dedicated hosts discovered via JS — `awv.kassenkompass.de` (self-hosted GTM proxy, nginx, `/gtm.js?id=GTM-TT4LBVMW`, root=400 noindex) + `load.awv.kassenkompass.de` (Cloudfla
- NEW kassenkompass.de: Funnel entry map from `param_passthrough.js` v=web1.0.0 (commented "kk-web-draft" refactor 2026-08-30) — only `bonusrechner*.php` + `termin.php` are app entry points; server-side coo
- CHANGED www.kassenkompass.de: Mirror header drift hypothesis dropped — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed
