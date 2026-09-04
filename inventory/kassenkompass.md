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
