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

## 2026-09-05 08:46:09 UTC
- NEW api.kassenkompass.de: v2 router sweep complete — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed
- NEW api.kassenkompass.de: Auth middleware map finalized — v1 majority + v2 share middleware A (`Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`); only `/user/{ext_id}` uses middleware
- NEW api.kassenkompass.de: X-API-Secret confirmed SOLE auth channel — `Authorization: Bearer`, `X-API-Key`, `X-Api-Token`, `api_key=` query all return 401 "erforderlich" on middleware A and B; no alternate
- NEW api.kassenkompass.de: Magic `KKX3382745` (sha256 bc2cb4e9…) and `X8372` (sha256 a4197524…) rejected (403) on ALL three auth paths including middleware-B and v2 — CRED_REUSE closed completely
- NEW kassenkompass.de: Funnel (`bonusrechner.php`) server-side mirrors raw pass-params into 1-year cookies with NO validation — alias map `jid|customerid→customerid`, `agn|connectionnumber→agenturnummer`, 
- NEW kassenkompass.de: Two new dedicated hosts discovered via JS — `awv.kassenkompass.de` (self-hosted GTM proxy, nginx, `/gtm.js?id=GTM-TT4LBVMW`, root=400 noindex) + `load.awv.kassenkompass.de` (Cloudfla
- NEW kassenkompass.de: Funnel entry map from `param_passthrough.js` v=web1.0.0 (commented "kk-web-draft" refactor 2026-08-30) — only `bonusrechner*.php` + `termin.php` are app entry points; server-side coo
- CHANGED www.kassenkompass.de: Mirror header drift hypothesis dropped — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed
- NEW awv.kassenkompass.de: GTM proxy probes completed — `/gtm.js?id=GTM-TT4LBVMW` returns 200 (nginx GTM proxy confirmed); `/gtm/debug` → 404; `/gtm/preview` → 404; root `/` → 404 (not 400); `load.awv.kass
- NEW awv.kassenkompass.de: No debug/preview/auth endpoints exposed on self-hosted GTM proxy — reduces config leakage surface
- CHANGED awv.kassenkompass.de: Root returns 404 not 400 noindex — prior "400 noindex" was inference; actual response is 404

## 2026-09-05 12:14:55 UTC
- CHANGED awv.kassenkompass.de: Root returns 404 not 400 noindex — prior "400 noindex" was inference; actual response is 404
- CHANGED awv.kassenkompass.de: GTM proxy debug/preview/auth endpoints all 404 — no standard GTM debug surface exposed; reduces config leakage surface

## 2026-09-05 15:32:54 UTC
- NEW awv.kassenkompass.de: Root returns 404 (not 400 noindex) — prior "400 noindex" was inference; actual response is 404
- NEW awv.kassenkompass.de: GTM proxy debug/preview/auth endpoints all 404 — no standard GTM debug surface exposed; reduces config leakage surface
- CHANGED api.kassenkompass.de: v2 router confirmed single-endpoint surface (only `insurance_info` registered via 24-name sweep)
- CHANGED api.kassenkompass.de: Auth middleware map finalized — v1 majority + v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt"); only `/user/{ext_id}` uses middleware
- CHANGED api.kassenkompass.de: X-API-Secret confirmed SOLE auth channel — `Authorization: Bearer`, `X-API-Key`, `X-Api-Token`, `api_key=` query all return 401 "erforderlich" on middleware A and B; no alternate
- CHANGED api.kassenkompass.de: Magic `KKX3382745` (sha256 bc2cb4e9…) and `X8372` (sha256 a4197524…) rejected (403) on ALL three auth paths including middleware-B and v2 — CRED_REUSE closed completely

## 2026-09-05 17:47:27 UTC
- NEW api.kassenkompass.de: v2 greedy-segment match confirmed — `/v2/insurance_info/1/extra`, `//1`, `%31`, `1%2fextra` all return HTTP 401 (reach auth handler); kk_id not validated at routing layer
- NEW kassenkompass.de: Funnel probes active — `bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` and `bonusrechner.php?jid=X&customerid=Y` return 200; Set-Cookie headers not yet captured in probe-resul
- NEW awv.kassenkompass.de: GTM proxy `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` returns 200 (dataLayer param accepted); `/gtm/debug`, `/gtm/preview`, root all 404
- CHANGED load.awv.kassenkompass.de: Consistent HTTP 403 (Cloudflare challenge) — not directly accessible
- CHANGED api.kassenkompass.de: v2 router sweep finalized — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed

## 2026-09-05 19:37:36 UTC
- NEW kassenkompass.net — canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical, form target `.de→.net`); sets same attribution cookies as `.de` then 302→.de. Prior sessions (all) inventoried only `.de`
- NEW bonusrechner.php uniquely sets unvalidated pass-params into 1-year cookies with 1 rps — re-confirmed live: `lizzen=test123`→`afilcode`, `jid=foo999`→`customerid`, `agn=bar888`→`agenturnummer`, `ppn=ba
- NEW Cookie attribute asymmetry: `afilcode` persisted WITHOUT `Secure`/`HttpOnly`; `customerid`/`agenturnummer`/`poolpartnernummer`/`advisorid`/`employeenumber` WITH `; Secure; HttpOnly; path=/` (HttpOnly 
- NEW Duplicate `customerid` Set-Cookie on same response when both `jid` and `customerid` present (`customerid=Y` from jid then `customerid=X` direct; last-wins, ambiguous consumption).
- CHANGED `frab` param set NO cookie on bonusrechner this cycle (probe `frab=fr33` → no Set-Cookie) — prior session alias map includes frab; needs recheck (possibly only on other entries).
- CHANGED No server-side HTML reflection of pass-params (grep of `TESTLIZ/JIDX/AGNY/PPNZ` in 200 body → 0 hits) — pure cookie mirroring, no stored/reflected XSS via these.
- NEW api.kassenkompass.de: v2 greedy-segment match confirmed — `/v2/insurance_info/1/extra`, `//1`, `%31`, `1%2fextra` all return HTTP 401 (reach auth handler); kk_id not validated at routing layer (probe-
- NEW awv.kassenkompass.de: GTM proxy `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` returns 200 (dataLayer param accepted); `/gtm/debug`, `/gtm/preview`, root all 404 (probe-results.md:126, 129-131)
- CHANGED load.awv.kassenkompass.de: Consistent HTTP 403 (Cloudflare challenge) — not directly accessible (probe-results.md:119, 128, 140)
- CHANGED api.kassenkompass.de: v2 router sweep finalized — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed (inventory.md:133, 143)
- CHANGED kassenkompass.de: Funnel probes active — `bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` and `bonusrechner.php?jid=X&customerid=Y` return 200; Set-Cookie headers not yet captured (probe-results

## 2026-09-05 21:47:42 UTC
- NEW Identified two untested api channels: `X-API-Secret=` as query-string/cookie (prior "sole channel" proof only covered header names + `api_key` query) — source-merge oracle never tested.
- NEW v2 route sweep gap: prior 24-name sweep only mirrored v1 names + user/partner/products/config/status/search/offers/rates — health/admin/internal/docs/schema/swagger/openapi/beta/staging never probed a
- NEW Funnel Set-Cookie value source (PHP `setcookie()` blocks CRLF vs `header()` allows) undetermined — CRLF probe discriminates; kassenkompass.net is the clean host (no Cloudflare filter, 302 returns Set-
- NEW kassenkompass.net — canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target .de→.net); sets identical unvalidated pass-param attribution cookies on .net then 302→.de; not pres
- NEW Cookie attribute asymmetry on kassenkompass.de: `afilcode` lacks Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernummer`/`advisorid`/`employeenumber` have `; Secure; HttpOnly; path=/`
- NEW Duplicate `customerid` Set-Cookie in single response when both `jid` and `customerid` passed (jid alias then direct; last-wins ambiguity)
- NEW `frab` param did NOT set cookie on bonusrechner this cycle (probe `frab=fr33` → no Set-Cookie) — prior alias map includes frab; entry-specific or context-dependent
- NEW No server-side HTML reflection of pass-params (grep of probe tokens in 200 body → 0 hits) — pure cookie mirroring, no stored/reflected XSS via these
- NEW api.kassenkompass.de: v2 greedy-segment match confirmed — `/v2/insurance_info/1/extra`, `//1`, `%31`, `1%2fextra` all return HTTP 401 (reach auth handler); kk_id not validated at routing layer
- NEW awv.kassenkompass.de: GTM proxy `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` returns 200 (dataLayer param accepted); `/gtm/debug`, `/gtm/preview`, root all 404
- CHANGED load.awv.kassenkompass.de: Consistent HTTP 403 (Cloudflare challenge) — not directly accessible
- CHANGED api.kassenkompass.de: v2 router sweep finalized — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed
- CHANGED kassenkompass.de: Funnel probes active — `bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` and `bonusrechner.php?jid=X&customerid=Y` return 200; Set-Cookie headers not yet captured

## 2026-09-05 23:48:57 UTC
- NEW v2 route enumeration extended to 42 names — 10 non-mirror infra names (health/admin/internal/swagger/schema/users/beta/docs/version/draft) + 8 German-domain names (tarife/anbieter/gkv/pkv/krankenkasse
- NEW Auth source-merge REJECTED — `?X-API-Secret=x` AND `Cookie: X-API-Secret=x` both return missing-header 401 ("erforderlich"/"fehlt") on middleware A (/insurance_info/1), B (/user/1), and v2 — X-API-Sec
- NEW CRLF injection REJECTED — .net Set-Cookie values percent-encoded on write (customerid=KKXCUST%0D%0AX-KK-Probe2...) and raw-CRLF values suppress the cookie entirely (lizzen→afilcode absent) — PHP setco
- NEW Auth middleware map extended to 15/15 — /cancel/{id} (POST, FG-Wechsel-Storno, "delegiert an kk_webapp") confirmed on middleware B ("X-API-Secret Header fehlt" + instance-first) like /user/{ext_id}; s
- NEW Alias map refined — frab sets NO cookie on termin.php (this cycle) NOR bonusrechner.php (prior cycle) → frab dropped from active alias set; lizzen→afilcode is bonusrechner-specific (termin.php emits n
- NEW .net mirror scoped — bonusrechner.php full mirror, termin.php subset (customerid/agenturnummer/poolpartnernummer), bonusrechner2.php + bonusrechner_alt.php mirror nothing; .net 302→.de carries NO para
- NEW api: v2 enumeration extended to 42 names (10 infra + 8 German-domain) — all structured router-404; `insurance_info` sole v2 route; primitive saturated.
- NEW api: `/cancel/{id}` confirmed on middleware B ("fehlt", instance-first) — B stack = {user/{ext_id}, cancel/{id}}; six unprobed data GETs all middleware A; 15/15 map complete.
- NEW api: Auth source-merge REJECTED — `?X-API-Secret=x` and `Cookie:` both missing-header 401 on A/B/v2; header strictly sole channel.
- NEW net: CRLF REJECTED — values percent-encoded on write (`customerid=KKXCUST%0D%0A...`) or cookie suppressed for raw CRLF (lizzen→afilcode absent); no splitting.
- NEW net: mirror scoped — bonusrechner2.php/_alt.php mirror nothing; termin.php subset only; 302→.de carries no params + host-only cookies ⇒ .net cookies unreadable by .de.
- NEW de: `frab` sets no cookie on either entry (2 sessions) — dropped from alias map; lizzen→afilcode is bonusrechner-specific.
- NEW kassenkompass.net — canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target .de→.net); sets identical unvalidated pass-param attribution cookies on .net then 302→.de; not pres
- NEW Cookie attribute asymmetry on kassenkompass.de: `afilcode` lacks Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernummer`/`advisorid`/`employeenumber` have `; Secure; HttpOnly; path=/`
- NEW Duplicate `customerid` Set-Cookie in single response when both `jid` and `customerid` passed (jid alias then direct; last-wins ambiguity)
- NEW `frab` param did NOT set cookie on bonusrechner this cycle (probe `frab=fr33` → no Set-Cookie) — prior alias map includes frab; entry-specific or context-dependent
- NEW No server-side HTML reflection of pass-params (grep of probe tokens in 200 body → 0 hits) — pure cookie mirroring, no stored/reflected XSS via these
- NEW api.kassenkompass.de: v2 greedy-segment match confirmed — `/v2/insurance_info/1/extra`, `//1`, `%31`, `1%2fextra` all return HTTP 401 (reach auth handler); kk_id not validated at routing layer
- NEW awv.kassenkompass.de: GTM proxy `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` returns 200 (dataLayer param accepted); `/gtm/debug`, `/gtm/preview`, root all 404
- CHANGED load.awv.kassenkompass.de: Consistent HTTP 403 (Cloudflare challenge) — not directly accessible
- CHANGED api.kassenkompass.de: v2 router sweep finalized — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed
- CHANGED kassenkompass.de: Funnel probes active — `bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` and `bonusrechner.php?jid=X&customerid=Y` return 200; Set-Cookie headers not yet captured

## 2026-09-06 04:12:41 UTC
- NEW kassenkompass.net discovered as canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target .de→.net); sets identical unvalidated pass-param attribution cookies on .net then 302→.
- NEW v2 route enumeration extended to 42 names (10 infra: health/admin/internal/swagger/schema/beta/staging/version/draft + 8 German-domain: tarife/anbieter/gkv/pkv/krankenkasse/kasse/category/categories) 
- NEW Auth source-merge REJECTED — X-API-Secret via query-string (`?X-API-Secret=x`) AND cookie (`Cookie: X-API-Secret=x`) both return missing-header 401 ("erforderlich"/"fehlt") on middleware A (/insurance
- NEW CRLF injection REJECTED on kassenkompass.net — Set-Cookie values percent-encoded on write (`customerid=KKXCUST%0D%0AX-KK-Probe2...`) or cookie suppressed for raw CRLF (lizzen→afilcode absent); PHP `se
- NEW Auth middleware map extended to 15/15 endpoints — /cancel/{id} (POST, FG-Wechsel-Storno, "delegiert an kk_webapp") confirmed on middleware B ("X-API-Secret Header fehlt", instance-first) with /user/{e
- NEW Alias map refined — frab sets NO cookie on termin.php (this cycle) NOR bonusrechner.php (prior cycle) → frab dropped from active alias set; lizzen→afilcode is bonusrechner-specific (termin.php emits n
- NEW .net mirror scoped — bonusrechner.php full mirror, termin.php subset (customerid/agenturnummer/poolpartnernummer), bonusrechner2.php + bonusrechner_alt.php mirror nothing; .net 302→.de carries NO para

## 2026-09-06 08:51:55 UTC
- NEW de funnel: full step map enumerated — bonusrechner_daten/fragen(2.1MB inline tariff data)/suche/vergleich2/abschluss all 200, wechsel2 302-guarded, alt 404 on .de; `bonusrechner_daten.php` is a SECOND
- NEW awv: client GTM container fully readable — GA4 G-RXB3GJEMRT with server_container_url=https://awv.kassenkompass.de (server-side GTM), FB pixel 360390300088445, purchase event (value 128 EUR / transact
- NEW de/inventory: kk-s3-01.s3.eu-central-1.amazonaws.com (public object reads; bucket listing AccessDenied); HubSpot portal 146866466 embedded on all pages; /login_auswahl.php chooser (kd/partner/kk only)
- CHANGED net: every *.php → 302 to https://kassenkompass.de root (no path preservation); param-less bonusrechner.php sets only PHPSESSID — .net name-oracle and cookie story closed.
- NEW kassenkompass.de/bonusrechner.php: Confirmed funnel parameter-to-cookie injection live — `lizenz→afilcode` (no Secure/HttpOnly), `jid→customerid`, `agn→agenturnummer`, `ppn→poolpartnernummer` all set 
- NEW kassenkompass.net/bonusrechner.php: Confirmed canonical IIS/10.0 backend mirrors identical cookie injection then 302→.de; cookies host-only on .net (not readable by .de)
- NEW api.kassenkompass.de/v2/insurance_info/{kk_id}: Confirmed middleware A shared with v1 majority (`"Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt"`); greedy segment match reaches a
- CHANGED v2 enumeration saturated at 42 names — only `insurance_info` registered; router-404 oracle confirmed
- CHANGED Auth source-merge closed — X-API-Secret via query/cookie both return missing-header 401 on all three stacks (A, B, v2)
- CHANGED Auth map 15/15 complete — /cancel/{id} joins middleware B with /user/{ext_id}; B = kk_webapp-delegation stack

## 2026-09-06 12:51:34 UTC

## 2026-09-06 16:14:12 UTC
- NEW bonusrechner_daten.php confirmed as second funnel entry with step-scoped alias map (jid/agn/ppn→1yr HttpOnly cookies, ignores lizzen/no afilcode)
- NEW awv.kassenkompass.de client container fully read: SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com public object reads (bucket listing AccessDenied) + HubSpot portal 146866466 embedded
- NEW kassenkompass.net all *.php → 302 bare-domain root (no path preservation); param-less GET sets only PHPSESSID
- NEW v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no XSS primitive
- NEW Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}
- CHANGED Funnel parameter-to-cookie injection confirmed live on both .de and .net bonusrechner.php (lizenz→afilcode, jid→customerid, agn→agenturnummer, ppn→poolpartnernummer)
- CHANGED api.v2/insurance_info confirmed middleware A shared with v1 majority; greedy segment match reaches auth handler; enumeration saturated at 42 names (insurance_info sole route)

## 2026-09-06 18:32:22 UTC

## 2026-09-06 20:53:42 UTC
- NEW bonusrechner_daten.php confirmed as second funnel entry with step-scoped alias map (jid/agn/ppn→1yr HttpOnly cookies, ignores lizzen/no afilcode)
- NEW bonusrechner_vergleich2.php as third mirror entry (jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; lizzen ignored)
- NEW termin.php + bonusrechner_suche.php as 4th/5th mirror entries (jid/agn/connectionnumber/employeenumber)
- NEW connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins ambiguity)
- NEW awv.kassenkompass.de client container fully read: SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com public object reads (bucket listing AccessDenied) + HubSpot portal 146866466 embedded
- NEW kassenkompass.net all *.php → 302 bare-domain root (no path preservation); param-less GET sets only PHPSESSID
- NEW v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no XSS primitive
- NEW Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}
- CHANGED Funnel parameter-to-cookie injection confirmed live on both .de and .net bonusrechner.php
- CHANGED api.v2/insurance_info confirmed middleware A shared with v1 majority; greedy segment match reaches auth handler; enumeration saturated at 42 names (insurance_info sole route)

## 2026-09-06 22:53:40 UTC
- NEW `kassenkompass.de/bonusrechner_daten.php` confirmed as 2nd funnel mirror entry — step-scoped alias map (jid/agn/ppn→1yr HttpOnly cookies; ignores lizenz/no afilcode) — live confirmed
- NEW `kassenkompass.de/bonusrechner_vergleich2.php` confirmed as 3rd mirror entry — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; connectionnumber→agenturnummer dual alias produces duplicate Se
- NEW `kassenkompass.de/termin.php` + `bonusrechner_suche.php` confirmed as 4th/5th mirror entries — jid/agn/connectionnumber/employeenumber→1yr HttpOnly; connectionnumber→agenturnummer dual alias duplicate
- NEW `kassenkompass.net` canonical IIS/10.0 backend — identical cookie injection then 302→.de; cookies host-only on .net (unreadable by .de) — live confirmed
- NEW `api.kassenkompass.de/v2/insurance_info/{kk_id}` greedy segment match confirmed — `/v2/insurance_info/{anything}` all reach auth handler (401); kk_id not validated at routing
- NEW `api.kassenkompass.de/v2` router-404 oracle saturated at 42 names — only `insurance_info` registered
- NEW Parser differential TESTED — null byte (`%00`), parameter pollution (last-wins), trailing space all handled IDENTICALLY on .de (Apache/PHP) and .net (IIS/PHP) — no differential; hypothesis REJECTED
- CHANGED Funnel stuffing surface expanded to ≥5 entry points (bonusrechner.php, bonusrechner_daten.php, bonusrechner_vergleich2.php, termin.php, bonusrechner_suche.php) with divergent alias maps per step
- CHANGED `bonusrechner.php` param for afilcode is `lizenz` (not `lizzen` per prior KB) — live confirmed
- CHANGED Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority

## 2026-09-07 00:53:46 UTC
- NEW `kassenkompass.de/bonusrechner_fragen.php` — 2.1MB inline tariff data response confirmed (probe 2026-09-06 12:51, 16:14); new funnel step with large data surface
- NEW `kassenkompass.de/bonusrechner_abschluss.php` — confirmed 200 response (probe 2026-09-06 16:14, 18:32); new funnel step, potential settlement submission endpoint
- NEW `awv.kassenkompass.de` client container fully read — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, `/g/collect` 400-on-invalid; SGTM supersedes "GTM proxy" labe
- NEW `kk-s3-01.s3.eu-central-1.amazonaws.com` — public object reads confirmed, bucket listing AccessDenied; 174 refs all `uploads/fraq/{qid}/{n}.png` question images (sequential qid); images-only, no sensi
- NEW `kassenkompass.net` parser differential TESTED — null byte (`%00`), parameter pollution (last-wins), trailing space all handled IDENTICALLY on .de (Apache/PHP) and .net (IIS/PHP); no differential; hyp
- NEW Funnel stuffing surface expanded to **≥5 entry points** with divergent alias maps: `bonusrechner.php` (lizenz→afilcode no Secure/HttpOnly; jid/agn/ppn→HttpOnly), `bonusrechner_daten.php` (jid/agn/ppn→
- NEW `bonusrechner.php` param for afilcode is `lizenz` (not `lizzen` per prior KB) — live confirmed
- NEW Auth map 15/15 complete — `/cancel/{id}` joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- NEW `api.kassenkompass.de/v2/insurance_info/{kk_id}` greedy segment match confirmed — `/v2/insurance_info/{anything}` all reach auth handler (401); kk_id not validated at routing
- NEW `api.kassenkompass.de/v2` router-404 oracle saturated at 42 names — only `insurance_info` registered
- CHANGED `api.kassenkompass.de/health/` — unchanged single unprotected endpoint (200 `{status:ok}`, Cloudflare fronting confirmed, PHP 8.4.3 x-powered-by); no env/version leak growth
- CHANGED Subdomain sweep ~80 names → only api/www/awv + load.awv exist; `kk_webapp` delegation is internal app-name, not hostname; no new inventory
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict

## 2026-09-07 05:58:14 UTC
- CHANGED bonusrechner_fragen.php probe executed and confirmed — 2.1MB inline tariff data response, new funnel step with large data surface (was [NEXT] PROBE in last leads)
- CHANGED v2 greedy segment match hypothesis demoted to PARKED (confidence 55) — Cloudflare/WAF normalizes path traversal sequences (%2e%2e%2f → 404) before router; only raw greedy segments (//, /extra, %31) re
- NEW bonusrechner_abschluss.php confirmed as 6th funnel step — 200 response, potential settlement submission endpoint
- NEW awv.kassenkompass.de fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png (sequential qid), images-only, no sensitive objects
- NEW GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict
- NEW Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname
- NEW Parser differential tested on .de vs .net — null byte (%00), parameter pollution (last-wins), trailing space all handled identically; no differential
- NEW Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority

## 2026-09-07 12:16:46 UTC
- NEW bonusrechner_abschluss.php confirmed as 6th funnel step — 200 response, potential settlement submission endpoint
- NEW awv.kassenkompass.de fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png (sequential qid), images-only, no sensitive objects
- NEW GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict
- NEW Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname
- NEW Parser differential tested on .de vs .net — null byte (%00), parameter pollution (last-wins), trailing space all handled identically; no differential
- NEW Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- CHANGED bonusrechner_fragen.php probe executed and confirmed — 2.1MB inline tariff data response, new funnel step with large data surface
- CHANGED v2 greedy segment match hypothesis demoted to PARKED (confidence 55) — Cloudflare/WAF normalizes path traversal sequences (%2e%2e%2f → 404) before router; only raw greedy segments (//, /extra, %31) re

## 2026-09-07 18:00:41 UTC
- NEW bonusrechner_abschluss.php confirmed as 6th funnel mirror entry — accepts lizenz→afilcode (no Secure/HttpOnly), jid→customerid, agn/connectionnumber→agenturnummer (dual alias), ppn→poolpartnernummer, 
- NEW bonusrechner_abschluss.php alias map is superset of prior steps — combines bonusrechner.php (lizenz/jid/agn/ppn) + vergleich2/termin/suche (connectionnumber/employeenumber); connectionnumber→agenturnu
- CHANGED Funnel stuffing surface now **7 entry points** (bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bonusrechner_abschluss.php, term
- CHANGED v2 greedy segment match hypothesis remains PARKED (confidence 55) — Cloudflare/WAF normalizes path traversal (%2e%2e%2f→404) before router; only raw greedy segments (//, /extra, %31) reach handler
- CHANGED Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority

## 2026-09-07 21:29:13 UTC
- NEW `bonusrechner_abschluss.php` confirmed as 7th funnel mirror entry (was 6th) — accepts `lizenz→afilcode` (no Secure/HttpOnly), `jid→customerid`, `agn/connectionnumber→agenturnummer` (dual alias), `ppn→
- NEW `bonusrechner_abschluss.php` alias map is superset of prior steps — combines `bonusrechner.php` (lizenz/jid/agn/ppn) + `vergleich2/termin/suche` (connectionnumber/employeenumber); `connectionnumber→ag
- CHANGED Funnel stuffing surface now **7 entry points** (`bonusrechner.php`, `bonusrechner_daten.php`, `bonusrechner_fragen.php`, `bonusrechner_suche.php`, `bonusrechner_vergleich2.php`, `bonusrechner_abschlus
- CHANGED v2 greedy segment match hypothesis remains PARKED (confidence 55) — Cloudflare/WAF normalizes path traversal (`%2e%2e%2f`→404) before router; only raw greedy segments (`//`, `/extra`, `%31`) reach han
- CHANGED Auth map 15/15 complete — `/cancel/{id}` joins middleware B; B = `kk_webapp`-delegation stack `{user, cancel}`; v2 shares middleware A with v1 majority

## 2026-09-07 23:48:01 UTC

## 2026-09-08 04:14:37 UTC

## 2026-09-08 09:16:02 UTC
- NEW verification path exists for top-ranked hypothesis: abschluss.php open self-registration (no CAPTCHA, create_account=1) enables automated cookie-stuffing→account-creation test without human interventi

## 2026-09-08 13:49:29 UTC
- NEW kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, no CAPTCHA, POST form) — provides automated verification s
- NEW kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumber→agenturnummer dual-alias duplicate; ppn→poolpartnernumm
- NEW kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbudgetsData, kombiboniData, pseudoKkIds=[99,100,101]) — unauthe
- NEW api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_fragen.php ucatKkData — BOLA cross-tenant read value downg
- NEW awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-only, no sensitive objects
- NEW kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie 
- NEW kassenkompass.de: Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- NEW kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Funnel stuffing surface expanded to 7 confirmed entry points (bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bonusrechner_absch
- CHANGED api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- CHANGED api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route; router-404 oracle confirmed
- CHANGED api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel (source-merge closed)
- CHANGED awv.kassenkompass.de: "GTM proxy" label superseded by SGTM (server-side GTM via Stape)
- NEW kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, no CAPTCHA, POST form) — provides automated verification s
- NEW kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumber→agenturnummer dual-alias duplicate; ppn→poolpartnernumm
- NEW kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbudgetsData, kombiboniData, pseudoKkIds=[99,100,101]) — unauthe
- NEW api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_fragen.php ucatKkData — BOLA cross-tenant read value downg
- NEW awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-only, no sensitive objects
- NEW kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie 
- NEW kassenkompass.de: Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- NEW kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Funnel stuffing surface expanded to 7 confirmed entry points (bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bonusrechner_absch
- CHANGED api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- CHANGED api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route; router-404 oracle confirmed
- CHANGED api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel (source-merge closed)
- CHANGED awv.kassenkompass.de: "GTM proxy" label superseded by SGTM (server-side GTM via Stape)

## 2026-09-08 17:45:17 UTC
- NEW kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, no CAPTCHA, POST form) — automated verification surface fo
- NEW kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumber→agenturnummer dual-alias duplicate; ppn→poolpartnernumm
- NEW kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbudgetsData, kombiboniData, pseudoKkIds=[99,100,101]) — unauthe
- NEW api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_fragen.php ucatKkData — BOLA cross-tenant read value downg
- NEW awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-only, no sensitive objects
- NEW kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie 
- NEW kassenkompass.de: Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- NEW kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Funnel stuffing surface expanded to 7 confirmed entry points (bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bonusrechner_absch
- CHANGED api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- CHANGED api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route; router-404 oracle confirmed
- CHANGED api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel (source-merge closed)
- CHANGED awv.kassenkompass.de: "GTM proxy" label superseded by SGTM (server-side GTM via Stape)

## 2026-09-08 20:23:43 UTC
- NEW kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, no CAPTCHA, POST form) — automated verification surface fo
- NEW kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumber→agenturnummer dual-alias duplicate; ppn→poolpartnernumm
- NEW kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbudgetsData, kombiboniData, pseudoKkIds=[99,100,101]) — unauthe
- NEW api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_fragen.php ucatKkData — BOLA cross-tenant read value downg
- NEW awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-only, no sensitive objects
- NEW kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie 
- NEW kassenkompass.de: Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- NEW kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Funnel stuffing surface expanded to 7 confirmed entry points (bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bonusrechner_absch
- CHANGED api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares middleware A with v1 majority
- CHANGED api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route; router-404 oracle confirmed
- CHANGED api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel (source-merge closed)
- CHANGED awv.kassenkompass.de: "GTM proxy" label superseded by SGTM (server-side GTM via Stape)

## 2026-09-08 22:50:10 UTC

## 2026-09-09 01:14:07 UTC
- CHANGED Current date 2026-09-09 01:09 UTC vs last KB entry 2026-09-08 22:50 UTC — no new passive recon since last session; surface stable
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- NEW 2.5-hour gap since last automated probes — potential for ephemeral changes (deployments, WAF rule updates) not captured

## 2026-09-09 06:12:53 UTC
- NEW awv.kassenkompass.de root returns 404 (not 400) with no body — SGTM container confirmed via Stape (ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid; 
- NEW kassenkompass.de/bonusrechner_abschluss.php form confirmed: POST method, fields email/password/password_confirm/create_account=1, no CAPTCHA, "Account erstellen" header — self-registration flow live
- NEW kassenkompass.de/bonusrechner_vergleich2.php sets device_id (1yr Secure HttpOnly) + expires catoint — new cookie observed vs prior sessions
- CHANGED api.kassenkompass.de root catalog stable (15 v1 endpoints, ver 1.0) + /v2/ catalog stable (sole insurance_info, ver 2.0) — no endpoint drift since 2026-09-07
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route confirmed again
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED 2.5-hour gap since last automated probes — potential for ephemeral changes (deployments, WAF rule updates) not captured
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces

## 2026-09-09 11:43:00 UTC

## 2026-09-09 15:36:36 UTC
- NEW awv.kassenkompass.de root confirmed 404 (not 400) with SGTM container fully characterized (Stape ahcfuvbcz, GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid)
- NEW bonusrechner_vergleich2.php sets new cookie `device_id` (1yr Secure HttpOnly) + `expires catoint` not seen in prior sessions
- NEW api.kassenkompass.de root catalog stable (15 v1 endpoints, ver 1.0) + /v2/ catalog stable (sole insurance_info, ver 2.0) — no endpoint drift since 2026-09-07
- NEW kassenkompass.de/bonusrechner_abschluss.php form confirmed: POST method, fields email/password/password_confirm/create_account=1, no CAPTCHA, "Account erstellen" header — self-registration flow live
- CHANGED 2.5-hour gap since last automated probes — potential for ephemeral changes (deployments, WAF rule updates) not captured
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route confirmed again
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps

## 2026-09-09 18:47:54 UTC
- NEW `kassenkompass.de/bonusrechner_vergleich2.php` sets new cookie `device_id` (1yr Secure HttpOnly) + `expires catoint` — not observed in prior sessions (probe-results 2026-09-09 06:12/15:36)
- NEW `kassenkompass.de/bonusrechner_abschluss.php` form confirmed: POST method, fields `email/password/password_confirm/create_account=1`, no CAPTCHA, "Account erstellen" header — self-registration flow li
- CHANGED `api.kassenkompass.de` root catalog stable (15 v1 endpoints, ver 1.0) + `/v2/` catalog stable (sole `insurance_info`, ver 2.0) — zero drift since 2026-09-07
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps — no new entries since 2026-09-07
- CHANGED `v2` router-404 oracle saturated at 42 names — `insurance_info` sole route confirmed again
- CHANGED Auth map 15/15 complete — `/cancel/{id}` middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (cache-buster/nonce drift only); cookie consumption strictly POST/portal-path

## 2026-09-09 21:39:23 UTC
- NEW bonusrechner_vergleich2.php sets new cookie `device_id` (1yr Secure HttpOnly) + `expires catoint` — not observed in prior sessions
- NEW bonusrechner_abschluss.php form confirmed: POST method, fields email/password/password_confirm/create_account=1, no CAPTCHA, "Account erstellen" header
- CHANGED api.kassenkompass.de root catalog stable (15 v1 + 1 v2 endpoint, ver 1.0/2.0) — zero drift since 2026-09-07
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential byte-identical (cache-buster/nonce drift only); cookie consumption strictly POST/portal-path
- CHANGED Session gap 2.5h since last probes — potential ephemeral changes not captured

## 2026-09-09 23:35:38 UTC

## 2026-09-10 01:32:22 UTC
- CHANGED Current date 2026-09-10 01:31 UTC vs last KB entry 2026-09-09 23:35 UTC — ~2h gap since last automated probes; potential ephemeral changes (deployments, WAF rules) not captured
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- NEW No new passive recon entries in KB since 2026-09-09 23:35 — surface stable per last aggregation

## 2026-09-10 06:44:21 UTC
- CHANGED Current date 2026-09-10 01:31 UTC vs last KB entry 2026-09-09 23:35 UTC — ~2h gap since last automated probes; potential ephemeral changes (deployments, WAF rules) not captured
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- NEW No new passive recon entries in KB since 2026-09-09 23:35 — surface stable per last aggregation

## 2026-09-10 11:58:17 UTC
- CHANGED Current date 2026-09-10 06:44 UTC vs last KB entry 2026-09-09 23:35 UTC — ~7h gap since last automated probes; potential ephemeral changes (deployments, WAF rules) not captured
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- NEW No new passive recon entries in KB since 2026-09-09 23:35 — surface stable per last aggregation

## 2026-09-10 16:15:52 UTC
- CHANGED Current date 2026-09-10 11:58 UTC vs last KB probe entry 2026-09-09 23:35 UTC — ~12h gap since last automated probes; potential ephemeral changes (deployments, WAF rules, SGTM container updates) not c
- CHANGED Phase remains POC, target api — cookie-stuffing chain (7 funnel entries) and v2 insurance_info remain top unverified attack surfaces
- NEW No new passive recon entries in KB since 2026-09-09 23:35 — surface stable per last aggregation
- NEW bonusrechner_vergleich2.php sets new cookie `device_id` (1yr Secure HttpOnly) + `expires catoint` — not observed in prior sessions (2026-09-09 probes)

## 2026-09-10 19:18:27 UTC

## 2026-09-10 21:45:49 UTC
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded — Partner Portal JS-delivered-secr
- NEW api.kassenkompass.de/ root: Returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r

## 2026-09-10 23:56:56 UTC
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded — Partner Portal JS-delivered-secr
- NEW api.kassenkompass.de/ root: Returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r

## 2026-09-11 04:25:26 UTC
- NEW api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded — Partner Portal JS-delivered-secr
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r

## 2026-09-11 09:20:20 UTC
- NEW api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded — Partner Portal JS-delivered-secr
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r

## 2026-09-11 13:40:20 UTC

## 2026-09-11 17:16:53 UTC
- NEW api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded — Partner Portal JS-delivered-secr
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r
- CHANGED api.kassenkompass.de root catalog stable (15 v1 endpoints, ver 1.0) + /v2/ catalog stable (sole insurance_info, ver 2.0) — zero drift since 2026-09-07
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route confirmed again
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps — no new entries since 2026-09-07
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (cache-buster/nonce drift only); cookie consumption strictly POST/portal-path

## 2026-09-11 19:54:26 UTC
- NEW api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r
- CHANGED api.kassenkompass.de root catalog stable (15 v1 endpoints, ver 1.0) + /v2/ catalog stable (sole insurance_info, ver 2.0) — zero drift since 2026-09-07
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route confirmed again
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps — no new entries since 2026-09-07
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (cache-buster/nonce drift only); cookie consumption strictly POST/portal-path

## 2026-09-11 22:29:04 UTC
- NEW api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- NEW kassenkompass.de/login_partner.php: Standard HTML login form (POST to self), no client-side JS bundle delivering X-API-Secret; only standard.js (UI utilities) loaded
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: Sets new `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — not observed prior to 2026-09-09; sole funnel step emitting device_id
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: Lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST, absent on GET; server validates Account-ID on form submission, not page r
- CHANGED api.kassenkompass.de root catalog stable (15 v1 endpoints, ver 1.0) + /v2/ catalog stable (sole insurance_info, ver 2.0) — zero drift since 2026-09-07
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route confirmed again
- CHANGED Auth map 15/15 complete — /cancel/{id} middleware B, v2 shares middleware A with v1 majority — stable
- CHANGED Funnel stuffing surface stable at 7 confirmed entry points with divergent alias maps — no new entries since 2026-09-07
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (cache-buster/nonce drift only); cookie consumption strictly POST/portal-path

## 2026-09-12 00:41:50 UTC
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured
- CHANGED api.kassenkompass.de/ root returns 200 with empty body (content-length: 0) but catalog still disclosed in JSON — structural change from prior full-body catalog; auth-gated endpoints unchanged
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php sets `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id (first observed 2026-09-09)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render

## 2026-09-12 05:10:26 UTC
- NEW api.kassenkompass.de/ root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalog; catalog disclosure without auth persists
- NEW ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php sets `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id (first observed 2026-09-09)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render

## 2026-09-12 09:29:44 UTC
- NEW api.kassenkompass.de/ root returns 200 with content-length: 0 but full JSON catalog (15 v1 endpoints, ver 1.0) in body — structural change from prior full-body catalog; catalog disclosure without auth
- NEW ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php sets `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id (first observed 2026-09-09)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php lead-gated POST confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render

## 2026-09-12 13:15:39 UTC

## 2026-09-12 16:27:24 UTC
- CHANGED api.kassenkompass.de/ root now returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 endpoints, ver 1.0) still disclosed in response body — structural change from prior full-body cata
- CHANGED kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit since 2026-09-07
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured

## 2026-09-12 18:50:03 UTC
- CHANGED api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 endpoints, ver 1.0) still disclosed in response body — structural change from prior full-body catalog;
- CHANGED kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit since 2026-09-07
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured

## 2026-09-12 21:23:53 UTC
- CHANGED api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 endpoints, ver 1.0) still disclosed in response body — structural change from prior full-body catalog;
- CHANGED kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit since 2026-09-07
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured
- CHANGED api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 endpoints, ver 1.0) still disclosed in response body — structural change from prior full-body catalog;
- CHANGED kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit since 2026-09-07
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured
- CHANGED ~2.5h since last automated probe batch (2026-09-12 18:50 UTC → now 21:20); probe-results tail ends at the 18:50 batch — all 3 standing smoke probes (fragen.php 200, bonusrechner.php stuffed 200, api r
- CHANGED triage run 2026-09-12-21-15 received an EMPTY lead payload (pipeline artifact) — no new agent leads to validate; lead-laguna/ling3/longcat/mimo are header-only, nemotron3 tail repeats known hypotheses
- CHANGED No KB entries after my 18:50 aggregation — catalogs (15+1 v2), auth map 15/15, 7 funnel mirrors, 2.1MB tariff payload, WAF posture all unchanged.
- NEW api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints, ver 1.0/2.0) still disclosed in response body — structural change from prior full-bo
- CHANGED kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit since 2026-09-07
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission, not page render
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes (deployments, WAF rules, SGTM container updates) not captured

## 2026-09-12 23:23:17 UTC
- NEW api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints, ver 1.0/2.0) still disclosed in response body — structural change from prior full-bo
- NEW kassenkompass.de/bonusrechner_fragen.php confirmed stable 2.1MB (2,158,150 bytes) tariff data response unauthenticated, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit — confirmed live at 20
- NEW kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on fo
- CHANGED ~24h gap since last automated probes (2026-09-11 22:29 UTC → 2026-09-12) — potential ephemeral changes not captured
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step with device_id, first observed 2026-09-09

## 2026-09-13 01:29:26 UTC
- NEW NO_DELTA — All live probes confirm knowledge base: api.kassenkompass.de/ returns 200 with content-length:0 + full 15+1 catalog; bonusrechner_fragen.php 2.1MB tariff data unauthenticated; bonusrechner_

## 2026-09-13 06:52:18 UTC
- NEW api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints) in response body — structural change from prior full-body catalog; catalog disclosur
- NEW kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id, confirmed live at 2026-09-13 06:47
- NEW kassenkompass.de/bonusrechner_fragen.php 2.1MB tariff payload (2,158,150 bytes) confirmed live — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modif
- NEW kassenkompass.de/bonusrechner_abschluss.php POST returns "Account-ID nicht gefunden" div (1 hit), GET returns 0 hits — server validates Account-ID on form submission only, lead gate confirmed
- CHANGED api.kassenkompass.de auth map 15/15 stable — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route, greedy segment match reaches auth handler (401)
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bon

## 2026-09-13 12:45:45 UTC
- NEW api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints) in response body — structural change from prior full-body catalog; catalog disclosur
- CHANGED kassenkompass.de/bonusrechner_fragen.php 2.1MB tariff payload (2,158,150 bytes) stable — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modified, no 
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id, confirmed live 2026-09-13 06:47
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on fo
- CHANGED api.kassenkompass.de auth map 15/15 stable — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route, greedy segment match reaches auth handler (401)
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bon
- CHANGED awv.kassenkompass.de SGTM container fully characterized — Stape (ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images, images-only, no sensitive objects
- CHANGED kassenkompass.net parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict

## 2026-09-13 16:59:38 UTC

## 2026-09-13 19:04:49 UTC

## 2026-09-13 21:28:39 UTC
- CHANGED pipeline: 8th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/now) consumed empty/header-only lead payloads — observability gap persists, no peer signal.
- CHANGED api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints) in response body — structural change from prior full-body catalog; catalog disclosur
- CHANGED kassenkompass.de/bonusrechner_fragen.php 2.1MB tariff payload (2,158,150 bytes) stable — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modified, no 
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id, confirmed live 2026-09-13 06:47
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on fo
- CHANGED api.kassenkompass.de auth map 15/15 stable — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route, greedy segment match reaches auth handler (401)
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bon
- CHANGED awv.kassenkompass.de SGTM container fully characterized — Stape (ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images, images-only, no sensitive objects
- CHANGED kassenkompass.net parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict
- CHANGED 5+ consecutive triage cycles consumed empty lead payloads — all peers header-only/repetition; observability gap, no signal

## 2026-09-13 23:38:19 UTC

## 2026-09-14 01:46:29 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php 2.1MB tariff payload (2,158,150 bytes) stable — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modified, no 
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id, confirmed live 2026-09-13 06:47
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on fo
- CHANGED api.kassenkompass.de auth map 15/15 stable — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route, greedy segment match reaches auth handler (401)
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bon
- CHANGED awv.kassenkompass.de SGTM container fully characterized — Stape (ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images, images-only, no sensitive objects
- CHANGED kassenkompass.net parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict
- CHANGED 5+ consecutive triage cycles consumed empty lead payloads — all peers header-only/repetition; observability gap, no signal
- NEW api.kassenkompass.de/ root returns HTTP 200 with `content-length: 0` but full JSON catalog (15 v1 + 1 v2 endpoints) in response body — structural header/body mismatch persists; catalog disclosure with
- NEW kassenkompass.de/bonusrechner_fragen.php 2.1MB tariff payload (2,158,150 bytes) confirmed live — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modif
- NEW kassenkompass.de/bonusrechner_vergleich2.php emits `device_id` cookie (1yr Secure HttpOnly SameSite=Lax) + `expires catoint` — sole funnel step emitting device_id, confirmed live
- NEW kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on fo
- CHANGED api.kassenkompass.de auth map 15/15 stable — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- CHANGED v2 router-404 oracle saturated at 42 names — insurance_info sole route, greedy segment match reaches auth handler (401)
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — bonusrechner.php, bonusrechner_daten.php, bonusrechner_fragen.php, bonusrechner_suche.php, bonusrechner_vergleich2.php, bon
- CHANGED awv.kassenkompass.de SGTM container fully characterized — Stape (ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 EUR, /g/collect 400-on-invalid
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images, images-only, no sensitive objects
- CHANGED kassenkompass.net parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and .net; no differential
- CHANGED Subdomain sweep ~80 names complete — only api/www/awv + load.awv exist; kk_webapp delegation is internal app-name, not hostname; no new inventory
- CHANGED GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standard.js?v= cache-buster + cfemail nonce drift only); cookie consumption strict

## 2026-09-14 07:13:37 UTC

## 2026-09-14 14:37:04 UTC

## 2026-09-14 19:40:15 UTC
- CHANGED api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — structural header/body mismatch confirmed live at 19:30 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 2,152,258 bytes (≈2.1MB) tariff payload confirmed live — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Mod
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- CHANGED api.kassenkompass.de/v2/ catalog stable — sole insurance_info endpoint, ver 2.0, greedy segment match reaches auth handler (401), enumeration saturated at 42 names
- CHANGED Auth map 15/15 drift-free — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — no new entries, no drift since 2026-09-07
- CHANGED 9th consecutive triage cycle consumed empty lead payloads — observability gap persists, no peer signal

## 2026-09-14 22:49:01 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: my live GET 22:47 (≤1 rps) measured decompressed body **2,152,258 B** vs recorded 2,158,150 (−5,892 B, 0.27%); tariff payload is NOT byte-static — drift since
- CHANGED fragen.php payload `lastchange` epochs are 2025 dates (1746314584=2025-05-03 … max 1766419026=2025-12-22) — prior KB "lastchange 2026-05-03" was an epoch mis-conversion.
- CHANGED pipeline: triage run-2026-09-14-22-17 = "No leads provided"; peer state files all 33-byte stubs (phase/target only) — **10th consecutive empty triage cycle**.

## 2026-09-15 01:21:14 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: live GET 22:47 measured 2,152,258 B vs recorded 2,158,150 (-5,892 B, 0.27%); tariff payload drifts on data refresh; sessionData still all-null; leak substance
- CHANGED kassenkompass.de/bonusrechner_fragen.php: per-KK lastchange epochs are 2025 (1746314584=2025-05-03, max 1766419026=2025-12-22); prior "2026-05-03" was epoch mis-conversion; data freshness ≤2025-12-22
- CHANGED pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap persists, no peer signal
- CHANGED api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — structural header/body mismatch confirmed; catalog disclosure without auth persists

## 2026-09-15 06:23:20 UTC
- NEW api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — structural header/body mismatch confirmed live at 06:18 UTC
- NEW kassenkompass.de/bonusrechner_fragen.php: live GET 2,152,258 bytes (matches 22:47 measurement, −5,892 B vs recorded 2,158,150); tariff payload drifts on data refresh
- NEW www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 bytes — tariff leak surface doubled apex+www
- NEW kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted confirmed live
- NEW kassenkompass.de/bonusrechner_abschluss.php: GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only
- CHANGED api.kassenkompass.de/v2/insurance_info/{kk_id}: 401 middleware A (shared with v1 majority); greedy segment match reaches auth handler; enumeration saturated at 42 names
- CHANGED Per-KK lastchange epochs confirmed 2025 (max 1766419026=2025-12-22); prior "2026-05-03" was epoch mis-conversion
- CHANGED Pipeline: 10th consecutive empty triage cycle — observability gap persists, no peer signal

## 2026-09-15 11:58:25 UTC
- NEW api.kassenkompass.de/ root: 06:18 probe confirms 200 + CL:0 + full 15+1 catalog in body — no drift since 22:47 09-14.
- NEW kassenkompass.de/bonusrechner_fragen.php: live 06:18 GET matches 2,152,258 B (−0.27% vs baseline 2,158,150); no-store, no ETag, no rate limit — unchanged.
- NEW www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 B — tariff leak doubled apex+www confirmed.
- CHANGED fragen.php 24h smoke: due after 22:47 09-15; last measurement 22:47 09-14 — window NOT yet met; hold.
- NEW api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — structural header/body mismatch confirmed live at 06:18 UTC
- NEW kassenkompass.de/bonusrechner_fragen.php: live GET 2,152,258 bytes (matches 22:47 measurement, −5,892 B vs recorded 2,158,150); tariff payload drifts on data refresh
- NEW www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 bytes — tariff leak surface doubled apex+www
- NEW kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted confirmed live
- NEW kassenkompass.de/bonusrechner_abschluss.php: GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only
- CHANGED api.kassenkompass.de/v2/insurance_info/{kk_id}: 401 middleware A (shared with v1 majority); greedy segment match reaches auth handler; enumeration saturated at 42 names
- CHANGED Per-KK lastchange epochs confirmed 2025 (max 1766419026=2025-12-22); prior "2026-05-03" was epoch mis-conversion
- CHANGED Pipeline: 10th consecutive empty triage cycle — observability gap persists, no peer signal

## 2026-09-15 16:49:34 UTC

## 2026-09-15 20:08:44 UTC

## 2026-09-15 23:00:42 UTC
- CHANGED 11th consecutive triage cycle (16:49 09-15) consumed empty/header-only peer leads — observability gap persists, zero peer signal
- CHANGED api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body at 16:49 — no drift since 06:18
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable at 2,152,258 B (±0.3% drift), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit
- CHANGED www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 B — leak surface confirmed doubled apex+www
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only
- CHANGED api.kassenkompass.de/v2/insurance_info/{kk_id}: 401 middleware A (shared with v1 majority); greedy segment match reaches auth handler; enumeration saturated at 42 names
- CHANGED Auth map 15/15 drift-free: /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — no new entries, no drift since 2026-09-07
- CHANGED Per-KK lastchange epochs confirmed 2025 (max 1766419026=2025-12-22); prior "2026-05-03" was epoch mis-conversion

## 2026-09-16 01:21:00 UTC
- CHANGED api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — no drift since 06:18 09-15
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable at 2,152,258 B (±0.3% drift), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate limit
- CHANGED www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 B — leak surface confirmed doubled apex+www
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only
- CHANGED api.kassenkompass.de/v2/insurance_info/{kk_id}: 401 middleware A (shared with v1 majority); greedy segment match reaches auth handler; enumeration saturated at 42 names
- CHANGED Auth map 15/15 drift-free: /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged
- CHANGED Funnel stuffing surface stable at 7 entry points with divergent alias maps — no new entries, no drift since 2026-09-07
- CHANGED Per-KK lastchange epochs confirmed 2025 (max 1766419026=2025-12-22); prior "2026-05-03" was epoch mis-conversion
- CHANGED 11th consecutive triage cycle consumed empty/header-only peer leads — observability gap persists, zero peer signal

## 2026-09-16 06:21:00 UTC
- CHANGED pipeline: 13th consecutive empty triage cycle (09-12 21:15 → 09-16 05:15) — peer leads (laguna/ling3/longcat/mimo) remain pure 85-row timestamp stubs; nemotron3 tail reprints own standing hypotheses; 

## 2026-09-16 11:58:17 UTC

## 2026-09-16 16:40:20 UTC
- NEW api.kassenkompass.de/ root: content-length: 0 header persists with full 15+1 JSON catalog in body — structural header/body mismatch confirmed live at 16:37 UTC
- NEW kassenkompass.de/bonusrechner_fragen.php: 2,152,680 B tariff payload confirmed live — ucatKkData/globalbudgetsData/kombiboniData/pseudoKkIds present, no-store+CF-DYNAMIC, no ETag/Last-Modified, no rat
- NEW www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,680 B — tariff leak surface doubled apex+www confirmed live
- NEW kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- NEW kassenkompass.de/bonusrechner_abschluss.php: GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only, lead gate confirmed
- NEW kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (afilcode non-HttpOnly, others HttpOnly)
- NEW api.kassenkompass.de/v2/insurance_info/{kk_id}: 401 middleware A (shared with v1 majority); greedy segment match reaches auth handler; enumeration saturated at 42 names
- NEW api.kassenkompass.de auth map 15/15 drift-free — /cancel/{id} middleware B, v2 shares middleware A with v1 majority, /sync/ HTTP-200 legacy body unchanged since 2026-09-03
- NEW kassenkompass.net not probed this cycle — parser differential, IIS/PHP backend, host-only cookies unchanged per KB
- NEW awv.kassenkompass.de SGTM container fully characterized per KB — Stape ahcfuvbcz, GA4 G-RXB3GJEMRT, FB 360390300088445, purchase 128 EUR, /g/collect 400-on-invalid
- CHANGED Pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, zero new signal

## 2026-09-16 20:04:45 UTC

## 2026-09-16 22:50:47 UTC

## 2026-09-17 01:21:27 UTC

## 2026-09-17 06:17:03 UTC

## 2026-09-17 11:59:06 UTC

## 2026-09-17 16:47:58 UTC

## 2026-09-17 20:10:15 UTC

## 2026-09-17 22:56:24 UTC

## 2026-09-18 01:11:07 UTC

## 2026-09-18 06:07:39 UTC

## 2026-09-18 11:37:09 UTC

## 2026-09-18 15:16:49 UTC
- NEW Scheduled probe window (≥2026-09-18 11:35 UTC) for `bonusrechner_fragen.php` 1-rps check has passed; no new probe results in KB since 11:37:09 aggregation
- NEW Peer pipeline remains silent — 14th+ consecutive triage cycle with header-only/stub leads; observability gap persists
- CHANGED Risk score holds at 85 — API catalog disclosure + 7-entry cookie stuffing funnel + 2.1MB tariff leak + v2 draft data surface unchanged

## 2026-09-18 18:39:29 UTC
- CHANGED Current time 2026-09-18 18:38 UTC vs last KB aggregation 11:37 UTC — ~7h gap; scheduled 1-rps probe window for bonusrechner_fragen.php elapsed with no new results in KB
- CHANGED Peer pipeline remains silent — 14th+ consecutive triage cycle with header-only/stub leads; observability gap persists

## 2026-09-18 21:18:22 UTC
- CHANGED Peer pipeline remains silent — 14th+ consecutive triage cycle with header-only/stub leads; observability gap persists
- CHANGED Scheduled 11:35 UTC probe window for bonusrechner_fragen.php elapsed with no new KB results
- CHANGED Next scheduled probe at ≥18:40 UTC (in ~1 minute) for bonusrechner_fragen.php 1-rps check

## 2026-09-18 23:30:14 UTC
- NEW Scheduled 1-rps probe window (≥2026-09-18 18:40 UTC) for `bonusrechner_fragen.php` elapsed with no new KB results — live probe at 2026-09-18 23:25 UTC confirms 2,152,708 B payload, `no-store`, `CF-DYN
- NEW `www.kassenkompass.de/bonusrechner_fragen.php` mirror identical 2,152,708 B — leak surface doubled apex+www confirmed live
- CHANGED `api.kassenkompass.de/` root: `content-length: 0` header persists with full 15+1 JSON catalog in body — structural header/body mismatch, disclosure substance unchanged
- CHANGED `api.kassenkompass.de/v2/insurance_info/{kk_id}` greedy segment match confirmed live (`/1/extra` → 401 middleware A); enumeration saturated at 42 names
- CHANGED `kassenkompass.de/bonusrechner.php` stuffing mirror re-confirmed live — `lizenz/jid/agn/ppn→4` 1yr cookies exact, attribute asymmetry intact (`afilcode` non-HttpOnly, others HttpOnly)
- CHANGED `kassenkompass.de/bonusrechner_vergleich2.php` emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `catoint` force-deleted — sole funnel step emitting `device_id`
- CHANGED `kassenkompass.de/bonusrechner_abschluss.php` GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on 
- CHANGED Peer pipeline remains silent — 14th+ consecutive triage cycle with header-only/stub leads; observability gap persists

## 2026-09-19 01:38:28 UTC
- NEW Next scheduled 1-rps probe window for `bonusrechner_fragen.php` opens at ≥2026-09-19 11:30 UTC (24h since last measurement at 11:30 09-18)
- CHANGED `api.kassenkompass.de/` root: `content-length: 0` header persists with full 15+1 JSON catalog in body — structural header/body mismatch, disclosure substance unchanged
- CHANGED `api.kassenkompass.de/v2/insurance_info/{kk_id}` greedy segment match confirmed live (`/1/extra` → 401 middleware A); enumeration saturated at 42 names
- CHANGED `kassenkompass.de/bonusrechner.php` stuffing mirror re-confirmed live — `lizenz/jid/agn/ppn→4` 1yr cookies exact, attribute asymmetry intact (`afilcode` non-HttpOnly, others HttpOnly)
- CHANGED `kassenkompass.de/bonusrechner_vergleich2.php` emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `catoint` force-deleted — sole funnel step emitting `device_id`
- CHANGED `kassenkompass.de/bonusrechner_abschluss.php` GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on 
- CHANGED Peer pipeline remains silent — 15th+ consecutive triage cycle with header-only/stub leads; observability gap persists

## 2026-09-19 06:41:21 UTC
- NEW `kassenkompass.de/bonusrechner_fragen.php` 24h smoke probe window opened at ≥2026-09-19 11:30 UTC (last measurement 11:30 09-18 at 2,152,680 B) — scheduled passive verification of tariff leak stabilit
- NEW `www.kassenkompass.de/bonusrechner_fragen.php` confirmed identical 2,152,708 B tariff payload at 23:25 09-18 — leak surface doubled apex+www, independent rate-limit buckets untested
- CHANGED `api.kassenkompass.de/` root: `content-length: 0` header persists with full 15+1 JSON catalog in body — structural header/body mismatch cosmetic only, disclosure substance unchanged since 2026-09-12
- CHANGED `api.kassenkompass.de/v2/insurance_info/{kk_id}` greedy segment match confirmed live (`/1/extra` → 401 middleware A); enumeration saturated at 42 names — no new routes
- CHANGED `kassenkompass.de/bonusrechner.php` stuffing mirror re-confirmed live — `lizenz/jid/agn/ppn→4` 1yr cookies exact, attribute asymmetry intact (`afilcode` non-HttpOnly, others HttpOnly)
- CHANGED `kassenkompass.de/bonusrechner_vergleich2.php` emits `device_id` (1yr Secure HttpOnly SameSite=Lax) + `catoint` force-deleted — sole funnel step emitting `device_id`, confirmed live
- CHANGED `kassenkompass.de/bonusrechner_abschluss.php` GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST (1 hit), absent on GET (0 hits); server validates Account-ID on 
- CHANGED Peer pipeline remains silent — 15th+ consecutive triage cycle with header-only/stub leads; observability gap persists

## 2026-09-19 11:38:46 UTC

## 2026-09-19 14:55:03 UTC

## 2026-09-19 17:59:55 UTC
- NEW Scheduled 1-rps probe window for `bonusrechner_fragen.php` at ≥2026-09-19 11:30 UTC has elapsed (now 14:55 UTC) but no new probe results in KB — live verification of tariff leak stability pending
- CHANGED All major surfaces stable: api catalog (15+
- NEW Scheduled 1-rps probe window for `bonusrechner_fragen.php` at ≥2026-09-19 11:30 UTC has elapsed (now 14:55 UTC) but no new probe results in KB — live verification of tariff leak stability pending
- CHANGED All major surfaces stable: api catalog (15+1, CL:0 header), v2 (insurance_info sole route, 42-name saturation), 7 funnel entry points with divergent alias maps, auth map 15/15 drift-free, tariff paylo
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07

## 2026-09-19 20:27:29 UTC
- NEW Scheduled 1-rps probe window for `bonusrechner_fragen.php` at ≥2026-09-19 11:30 UTC elapsed (now 17:59 UTC) with no new KB results — live verification of tariff leak stability pending
- CHANGED All major surfaces stable: api catalog (15+1, CL:0 header), v2 (insurance_info sole route, 42-name saturation), 7 funnel entry points with divergent alias maps, auth map 15/15 drift-free, tariff paylo
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07

## 2026-09-19 22:33:47 UTC
- NEW Live probe: `kassenkompass.de/bonusrechner_fragen.php` returns HTTP 200, 2,152,708 bytes, `cache-control: no-store, no-cache, must-revalidate`, `cf-cache-status: DYNAMIC`, no ETag/Last-Modified — tari
- NEW Live probe: `www.kassenkompass.de/bonusrechner_fragen.php` identical 2,152,708 bytes, same headers — mirror surface doubled confirmed
- NEW Live probe: `api.kassenkompass.de/` returns HTTP 200, `content-length: 0` header but full 15-endpoint JSON catalog in body — structural header/body mismatch persists
- CHANGED Scheduled 1-rps probe window for `bonusrechner_fragen.php` at ≥2026-09-19 11:30 UTC elapsed — live verification complete
- CHANGED All major surfaces stable: api catalog (15+1, CL:0), v2 (insurance_info sole route, 42-name saturation), 7 funnel entries, auth map 15/15 drift-free
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists

## 2026-09-20 00:26:14 UTC
- NEW Live probe: `kassenkompass.de/bonusrechner_fragen.php` HTTP 200, 2,152,708 bytes, `cache-control: no-store`, `cf-cache-status: DYNAMIC`, no ETag/Last-Modified — tariff leak stable
- NEW Live probe: `www.kassenkompass.de/bonusrechner_fragen.php` identical 2,152,708 bytes, same headers — mirror surface doubled confirmed
- NEW Live probe: `api.kassenkompass.de/` HTTP 200, `content-length: 0` header but full 1167-byte JSON catalog (15 v1 + 1 v2 endpoints, ver 1.0/2.0) in body — structural header/body mismatch persists
- NEW Live probe: `api.kassenkompass.de/v2/insurance_info/1/extra` HTTP 401 middleware A — greedy segment match confirmed, enumeration saturated at 42 names
- NEW Live probe: `kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` sets 4 attribution cookies (afilcode non-HttpOnly, others HttpOnly) — stuffing mirror re-confirmed live
- NEW Live probe: `kassenkompass.de/bonusrechner_vergleich2.php` sets `device_id` (1yr Secure HttpOnly SameSite=Lax) + force-deletes `catoint` — sole funnel step emitting device_id confirmed
- NEW Live probe: `kassenkompass.de/bonusrechner_abschluss.php` GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only, lead gate confirmed
- CHANGED All major surfaces stable since 2026-09-07: api catalog (15+1, CL:0), v2 (insurance_info sole route, 42-name saturation), 7 funnel entries with divergent alias maps, auth map 15/15 drift-free
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07

## 2026-09-20 05:28:10 UTC
- NEW Live probe: `kassenkompass.de/bonusrechner_fragen.php` HTTP 200, 2,152,708 bytes, `cache-control: no-store`, `cf-cache-status: DYNAMIC`, no ETag/Last-Modified — tariff leak stable
- NEW Live probe: `www.kassenkompass.de/bonusrechner_fragen.php` identical 2,152,708 bytes, same headers — mirror surface doubled confirmed
- NEW Live probe: `api.kassenkompass.de/` HTTP 200, `content-length: 0` header but full 1167-byte JSON catalog (15 v1 + 1 v2 endpoints, ver 1.0/2.0) in body — structural header/body mismatch persists
- NEW Live probe: `api.kassenkompass.de/v2/insurance_info/1/extra` HTTP 401 middleware A — greedy segment match confirmed, enumeration saturated at 42 names
- NEW Live probe: `kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789` sets 4 attribution cookies (afilcode non-HttpOnly, others HttpOnly) — stuffing mirror re-confirmed live
- NEW Live probe: `kassenkompass.de/bonusrechner_vergleich2.php` sets `device_id` (1yr Secure HttpOnly SameSite=Lax) + force-deletes `catoint` — sole funnel step emitting device_id confirmed
- NEW Live probe: `kassenkompass.de/bonusrechner_abschluss.php` GET 0 hits "Account-ID nicht gefunden", POST 1 hit — server validates Account-ID on form submission only, lead gate confirmed
- CHANGED All major surfaces stable since 2026-09-07: api catalog (15+1, CL:0), v2 (insurance_info sole route, 42-name saturation), 7 funnel entries with divergent alias maps, auth map 15/15 drift-free
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07
- CHANGED Time advanced to 2026-09-20 05:26 UTC — ~5h since last live probes (00:24 UTC); scheduled 24h smoke window for `bonusrechner_fragen.php` next rotation ≥22:33 UTC (per 09-19 22:33 measurement)
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable per 00:24 live probes

## 2026-09-20 10:17:07 UTC
- CHANGED Time advanced to 2026-09-20 05:26 UTC — ~5h since last live probes (00:24 UTC); scheduled 24h smoke window for `bonusrechner_fragen.php` next rotation ≥22:33 UTC (per 09-19 22:33 measurement)
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable per 00:24 live probes
- CHANGED Time 05:26 UTC vs last probes 00:24 09-20 — 5h quiet; 24h fragen smoke rotation due window ≥22:33 UTC 09-20 not yet reached
- CHANGED Peer pipeline: 16th+ consecutive triage cycle (run-2026-09-20-07-01 "No leads to triage", 01-36 incomplete) — laguna/ling3/longcat timestamp stubs, nemo reprint, no peer signal
- CHANGED All live surfaces stable per 00:24 batch — no new attack surface introduced since 2026-09-07
- CHANGED api.kassenkompass.de/ root: content-length header now accurately reports 1167 (was 0 with full body) — cosmetic header/body mismatch resolved; catalog disclosure without auth persists
- CHANGED bonusrechner_fragen.php: 24h smoke model holds at 2,152,708 B (±0.0% vs 09-19 22:33); drift-on-refresh within ±0.3% window maintained across 6 rotation windows
- CHANGED www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,708 B payload confirmed — mirror surface doubled, independent rate-limit buckets untested
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable per live probes at 10:10 UTC
- CHANGED Peer pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal

## 2026-09-20 14:26:48 UTC
- CHANGED Time ~10:17 UTC 09-20 vs last live probes 10:10-10:11 UTC 09-20 (within the hour) — api root now serves accurate content-length 1167 (was CL:0-with-body), catalog substance unchanged; fragen.php + www
- CHANGED 24h fragen smoke rotation not yet due — last measurement 2,152,708 B @22:33 09-19; window opens ≥22:33 UTC 09-20 (~12h away); hold.
- CHANGED Peer pipeline: 16th+ consecutive triage cycle (run-2026-09-20-10-17); laguna/ling3/longcat stub-only, nemo reprint; observability gap persists, zero new signal.

## 2026-09-20 17:36:52 UTC

## 2026-09-20 19:49:07 UTC

## 2026-09-20 22:22:30 UTC

## 2026-09-21 00:23:18 UTC
- CHANGED Current time 2026-09-20 22:22 UTC vs last live probes 22:21 UTC — ~1 minute gap; all surfaces stable per 22:21 batch
- CHANGED 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC (per 09-19 22:33 measurement at 2,152,708 B) — not yet reached (11 min away)
- CHANGED Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable

## 2026-09-21 05:32:29 UTC
- CHANGED Current time 2026-09-20 22:22 UTC vs last live probes 22:21 UTC — ~1 minute gap; all surfaces stable per 22:21 batch
- CHANGED 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC (per 09-19 22:33 measurement at 2,152,708 B) — not yet reached (11 min away)
- CHANGED Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable
- CHANGED Time advanced ~7h since last live probes (2026-09-20 22:21 UTC → 2026-09-21 05:29 UTC); 24h fragen.php smoke rotation window (≥22:33 UTC 09-20) has elapsed with no new KB results
- CHANGED Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable per last live probes at 22:21 UTC

## 2026-09-21 11:09:38 UTC
- CHANGED Time advanced ~7h since last live probes (2026-09-20 22:21 UTC → 2026-09-21 05:29 UTC); 24h fragen.php smoke rotation window (≥22:33 UTC 09-20) has elapsed with no new KB results
- CHANGED Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable per last live probes at 22:21 UTC

## 2026-09-21 17:09:33 UTC
- CHANGED Time advanced ~7h since last live probes (2026-09-20 22:21 UTC → 2026-09-21 05:29 UTC); 24h fragen.php smoke rotation window (≥22:33 UTC 09-20) has elapsed with no new KB results
- CHANGED Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable per last live probes at 22:21 UTC

## 2026-09-21 21:09:47 UTC
- CHANGED Time now 2026-09-21 21:08:34 UTC; last live measurement 2,152,708 B @ 22:21 09-20 — 24h smoke rotation window opens ≥22:21 09-21 (~1h 12m remaining); hold maintained, no premature probe-noise.
- CHANGED Peer pipeline: 18th consecutive empty triage cycle (run-2026-09-21-18-48 "No leads provided"; laguna/ling3/longcat timestamp-only stubs, mimo empty, nemotron3 reprint) — observability gap persists, ze
- CHANGED No new attack surface since 2026-09-07 — api catalog (15+1 v2), auth map 15/15, v2 42-name saturation, 7 funnel mirrors all drift-free per last batch.
- NEW Time advanced ~4h since last aggregation (2026-09-21 17:09 → 2026-09-21 21:08 UTC); 24h fragen.php smoke rotation window (≥22:33 UTC 09-20) elapsed with no new KB results
- NEW Peer pipeline: 17th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal
- NEW No new attack surface introduced since 2026-09-07 — all major surfaces stable per last live probes at 2026-09-20 22:21 UTC

## 2026-09-22 00:18:51 UTC
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:33 UTC 09-20 per 09-19 22:33 measurement at 2,152,708 B; window ≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no
- CHANGED Peer pipeline: 18th consecutive triage cycle with header-only/stub leads (run-2026-09-21-18-48 empty; laguna/ling3/longcat timestamp stubs, mimo empty, nemotron3 reprint) — observability gap persists,
- CHANGED Time advanced ~4h since last aggregation (2026-09-21 17:09 → 2026-09-21 21:08 UTC); all major surfaces stable per last live probes at 2026-09-20 22:21 UTC
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:33 UTC 09-20 per 09-19 22:33 measurement at 2,152,708 B; window ≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no
- CHANGED Peer pipeline: 18th consecutive triage cycle with header-only/stub leads (run-2026-09-21-18-48 empty; laguna/ling3/longcat timestamp stubs, mimo empty, nemotron3 reprint) — observability gap persists,
- CHANGED Time advanced ~4h since last aggregation (2026-09-21 17:09 → 2026-09-21 21:08 UTC); all major surfaces stable per last live probes at 2026-09-20 22:21 UTC

## 2026-09-22 05:10:49 UTC
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue
- CHANGED Peer pipeline: 18th consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- CHANGED Time advanced ~26h since last live probes (2026-09-20 22:21 → 2026-09-22 00:18); all major surfaces stable per last live probes

## 2026-09-22 10:07:49 UTC
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue
- CHANGED Peer pipeline: 18th consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- CHANGED Time advanced ~26h since last live probes (2026-09-20 22:21 → 2026-09-22 00:18); all major surfaces stable per last live probes

## 2026-09-22 15:08:55 UTC
- CHANGED `kassenkompass.de/bonusrechner_fragen.php`: 24h smoke rotation window elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue. Live probe at 15:02 UTC confir
- CHANGED `www.kassenkompass.de/bonusrechner_fragen.php`: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live.
- CHANGED `api.kassenkompass.de/`: Root returns HTTP 200, `content-length: 0` header but full 1167-byte JSON catalog (15 v1 + 1 v2 endpoints, ver 1.0/2.0) in body — structural header/body mismatch persists, cat
- CHANGED `api.kassenkompass.de/sync/`: Returns HTTP 200 with auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` instead of 401 — behavioral misconfiguration persists.
- CHANGED `api.kassenkompass.de/v2/insurance_info/1/extra`: Returns HTTP 401 middleware A (RFC 9457) — greedy segment match confirmed, enumeration saturated at 42 names.
- CHANGED Two distinct 403 error messages confirmed live: middleware B (`/user/1`) → "Ungültiger X-API-Secret"; middleware A (`/insurance_info/1`) → "Der bereitgestellte X-API-Secret ist ungültig oder nicht ber
- CHANGED Peer pipeline: 18th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal.
- CHANGED Time advanced ~26h since last live probes (2026-09-20 22:21 → 2026-09-22 15:02); all major surfaces stable per last live probes.

## 2026-09-22 19:02:50 UTC

## 2026-09-22 22:02:50 UTC

## 2026-09-23 00:25:34 UTC
- CHANGED Time advanced ~7h since last live probes (2026-09-22 15:02 UTC → 2026-09-22 22:02 UTC); all major surfaces stable per last live batch
- CHANGED 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue
- CHANGED Peer pipeline: 18th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — api catalog (15+1), v2 (42-name saturation), 7 funnel mirrors, auth map 15/15 all drift-free

## 2026-09-23 05:22:43 UTC

## 2026-09-23 10:13:02 UTC

## 2026-09-23 15:09:45 UTC
- NEW Time advanced ~7h since last live probes (2026-09-22 15:02 UTC → 2026-09-22 22:02 UTC per 00:25 lead, now 10:13 UTC); all major surfaces stable per last live batch
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue
- NEW Peer pipeline: 18th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- NEW No new attack surface introduced since 2026-09-07 — api catalog (15+1), v2 (42-name saturation), 7 funnel mirrors, auth map 15/15 all drift-free
- CHANGED Bigpickle NEXT: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:23 UTC baseline → due ≥00:23 09-24
- CHANGED Nemotron3 NEXT: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps

## 2026-09-23 19:09:28 UTC
- NEW Time advanced ~4h since last aggregation (2026-09-23 15:09 → 2026-09-23 19:07 UTC); all major surfaces stable per last live batch (2026-09-22 15:02 UTC)
- NEW 24h smoke rotation window for `kassenkompass.de/bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — no new KB results recorded; probe overdue
- NEW Peer pipeline: 19th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- NEW No new attack surface introduced since 2026-09-07 — api catalog (15+1), v2 (42-name saturation), 7 funnel mirrors, auth map 15/15 all drift-free
- CHANGED Bigpickle NEXT: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:23 UTC baseline → due ≥00:23 09-24
- CHANGED Nemotron3 NEXT: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps

## 2026-09-23 22:27:21 UTC
- NEW Current time 2026-09-23 22:23 UTC vs last KB live probes 2026-09-22 15:02 UTC — ~31h gap; all major surfaces reconfirmed live in this check
- CHANGED `kassenkompass.de/bonusrechner_abschluss.php` POST lead gate requires full form submission (email/password/password_confirm/create_account=1) — empty POST returns 0 "Account-ID nicht gefunden", only v
- CHANGED 24h smoke rotation window for `bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — payload stable at 2,152,708 B apex+www; no new KB results recorded; probe overdue
- CHANGED Peer pipeline: 20th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — api catalog (15+1), v2 (42-name saturation), 7 funnel mirrors, auth map 15/15 all drift-free per live probes

## 2026-09-24 00:54:04 UTC
- NEW Current time 2026-09-23 22:23 UTC vs last KB live probes 2026-09-22 15:02 UTC — ~31h gap; all major surfaces reconfirmed live in this check
- CHANGED `kassenkompass.de/bonusrechner_abschluss.php` POST lead gate requires full form submission (email/password/password_confirm/create_account=1) — empty POST returns 0 "Account-ID nicht gefunden", only v
- CHANGED 24h smoke rotation window for `bonusrechner_fragen.php` elapsed (≥22:21 UTC 09-21 per 09-20 22:21 measurement) — payload stable at 2,152,708 B apex+www; no new KB results recorded; probe overdue
- CHANGED Peer pipeline: 20th+ consecutive triage cycle with header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — api catalog (15+1), v2 (42-name saturation), 7 funnel mirrors, auth map 15/15 all drift-free per live probes

## 2026-09-24 06:01:58 UTC

## 2026-09-24 11:40:50 UTC

## 2026-09-24 15:57:01 UTC

## 2026-09-24 19:57:00 UTC

## 2026-09-24 23:10:32 UTC

## 2026-09-25 01:39:43 UTC

## 2026-09-25 06:40:11 UTC

## 2026-09-25 12:27:48 UTC

## 2026-09-25 17:22:08 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 24h smoke 01:37 09-25 — apex+www both 200 / 2,152,708 B exact, 1-byte cfemail-nonce diff @712; byte-frozen 7+ consecutive windows (09-18→09-25); no-store+CF-D
- CHANGED api.kassenkompass.de: root 200 / content-length 1167 == body 1167 at 01:37 09-25 (accurate-CL variant of persistent cosmetic drift class CL:0→absent→accurate); 15+1 catalog substance unchanged; auth m
- CHANGED api.kassenkompass.de/v2/insurance_info/: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at routing
- CHANGED kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (afilcode non-HttpOnly, others HttpOnly)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on valid form POST; server validates Account-ID on form submission, not page render; le
- CHANGED kassenkompass pipeline: 22nd+ consecutive triage cycle consumed header-only/stub peer leads — observability gap persists, zero new signal; no new attack surface anywhere

## 2026-09-25 20:43:07 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 24h smoke 01:37 09-25 — apex+www both 200 / 2,152,708 B exact, 1-byte cfemail-nonce diff @712; byte-frozen 7+ consecutive windows (09-18→09-25); no-store+CF-D
- CHANGED api.kassenkompass.de: root 200 / content-length 1167 == body 1167 at 01:37 09-25 (accurate-CL variant of persistent cosmetic drift class CL:0→absent→accurate); 15+1 catalog substance unchanged; auth m
- CHANGED api.kassenkompass.de/v2/insurance_info/: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at routing
- CHANGED kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (afilcode non-HttpOnly, others HttpOnly)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on valid form POST; server validates Account-ID on form submission, not page render; le
- CHANGED kassenkompass pipeline: 22nd+ consecutive triage cycle consumed header-only/stub peer leads — observability gap persists, zero new signal; no new attack surface anywhere
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com has a reliable existence oracle never previously established: real key -> 200 (public read, full body), absent key -> 403 AccessDenied XML (~243-263B, length var
- CHANGED kk-s3-01 qid space is 1..180, not 1..174: qid 175-180 return 200 with no page reference (qid 180 -> 200, qid 181 -> 403). All of 174/175/180 share ETag 52f04d114ad9a1ab359ff47d672bbd0b / 747,082 B / L
- NEW kk-s3-01 n-dimension extends beyond 1: /uploads/fraq/60/2.png -> 200 (1,051,319 B) while qid 5 n=2 and qid 60 n=3 are 403 — multi-image questionnaire items exist; the n-axis is unenumerated.
- NEW kk-s3-01 non-image/sensitive objects all AccessDenied: .env, .git/config, web.config (root and /api/), backup.sql, dump.sql, error_log, phpinfo.php. /uploads/ returns 200 but is a zero-byte S3 autoind
- CHANGED kassenkompass.net has NO existence oracle: every app-handled path returns 302, not 404 — both .php and non-.php (/api/web.config, /api/.env, /api/index.php, /api/sync.php, /api/insurance_info.php all 
- CHANGED api.kassenkompass.de/health/ re-confirmed unchanged: 200, 22 B application/json, server: cloudflare, x-powered-by: PHP/8.4.3, XFO DENY, no rate limit observed. Auth map 15/15 and v2 42-name saturation
- NEW Tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3% — drift-on-refresh model confirmed stable
- NEW API root header-shape drift class confirmed cosmetic: CL:0→absent→accurate 1167 B, catalog substance unchanged through 24+ cycles
- NEW All auth maps (15/15), v2 enumeration (42 names saturated), 7 funnel entry points, stuffing mirrors — zero drift since 2026-09-07
- NEW Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED NEXT probe windows: nemotron3 alternating 20×1-rps GET on apex+www fragen.php; bigpickle single GET at ≥2026-09-26 01:37 UTC

## 2026-09-25 23:35:15 UTC
- NEW Tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3% — drift-on-refresh model confirmed stable
- NEW API root header-shape drift class confirmed cosmetic: CL:0→absent→accurate 1167 B, catalog substance unchanged through 24+ cycles
- NEW All auth maps (15/15), v2 enumeration (42 names saturated), 7 funnel entry points, stuffing mirrors — zero drift since 2026-09-07
- NEW Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED NEXT probe windows: nemotron3 alternating 20×1-rps GET on apex+www fragen.php; bigpickle single GET at ≥2026-09-26 01:37 UTC
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis extends to 1..180 (6 IDs beyond page-referenced set), all byte-identical duplicates (ETag 52f04d11..., 747,082 B, 2025-10-28); n-dimension extends beyo
- NEW kassenkompass.net: blanket 302 on every app-handled path (both .php and non-.php) → no existence oracle; cannot be used for origin-bypass differential testing
- CHANGED api.kassenkompass.de: root header-shape drift class confirmed cosmetic (CL:0→absent→accurate 1167 B), catalog substance unchanged through 24+ cycles; auth map 15/15 drift-free
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-26 02:04:56 UTC
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 24h smoke 01:37 09-25 — apex+www both 200 / 2,152,708 B exact, 1-byte cfemail-nonce diff @712; byte-frozen 7+ consecutive windows (09-18→09-25); no-store+CF-D
- CHANGED api.kassenkompass.de: root 200 / content-length 1167 == body 1167 at 01:37 09-25 (accurate-CL variant of persistent cosmetic drift class CL:0→absent→accurate); 15+1 catalog substance unchanged; auth m
- CHANGED api.kassenkompass.de/v2/insurance_info/: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at routing
- CHANGED kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (afilcode non-HttpOnly, others HttpOnly)
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on valid form POST; server validates Account-ID on form submission, not page render; le
- CHANGED kassenkompass pipeline: 22nd+ consecutive triage cycle consumed header-only/stub peer leads — observability gap persists, zero new signal; no new attack surface anywhere
- NEW Tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3% — drift-on-refresh model confirmed stable
- NEW API root header-shape drift class confirmed cosmetic: CL:0→absent→accurate 1167 B, catalog substance unchanged through 24+ cycles
- NEW All auth maps (15/15), v2 enumeration (42 names saturated), 7 funnel entry points, stuffing mirrors — zero drift since 2026-09-07
- NEW Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED NEXT probe windows: nemotron3 alternating 20×1-rps GET on apex+www fragen.php; bigpickle single GET at ≥2026-09-26 01:37 UTC
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis extends to 1..180 (6 IDs beyond page-referenced set), all byte-identical duplicates (ETag 52f04d11..., 747,082 B, 2025-10-28); n-dimension extends beyo
- NEW kassenkompass.net: blanket 302 on every app-handled path (both .php and non-.php) → no existence oracle; cannot be used for origin-bypass differential testing
- CHANGED api.kassenkompass.de: root header-shape drift class confirmed cosmetic (CL:0→absent→accurate 1167 B), catalog substance unchanged through 24+ cycles; auth map 15/15 drift-free
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis extends to 1..180 (6 IDs beyond page-referenced set), all byte-identical duplicates (ETag 52f04d11..., 747,082 B, 2025-10-28); n-dimension extends beyo
- NEW kassenkompass.net: blanket 302 on every app-handled path (both .php and non-.php) → no existence oracle; cannot be used for origin-bypass differential testing
- CHANGED api.kassenkompass.de: root header-shape drift class confirmed cosmetic (CL:0→absent→accurate 1167 B), catalog substance unchanged through 24+ cycles; auth map 15/15 drift-free
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED Peer pipeline: 22+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: added to PRIO list at 5.80 (attack_surface=6, business_value=5, tech_exposure=5, gate_ease=10, cloud_surface=8, freshness=7)

## 2026-09-26 07:36:09 UTC
- NEW Sustained 1-rps scraping of `bonusrechner_fragen.php` confirmed: 20 alternating apex/www requests at 1 rps all return HTTP 200 / 2,152,708 B — no 429, no WAF block, no rate limit
- NEW S3 bucket qid axis extends to 180 (6 IDs beyond page-referenced 174), all byte-identical duplicates (ETag 52f04d11..., 747,082 B, 2025-10-28); n-dimension extends beyond n=1 (qid 60 n=2 returns 1,051,
- CHANGED api.kassenkompass.de root: content-length header now accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 23rd consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-26 12:31:13 UTC
- NEW Sustained 1-rps scraping of `bonusrechner_fragen.php` confirmed: 20 alternating apex/www requests at 1 rps all return HTTP 200 / 2,152,708 B — no 429, no WAF block, no rate limit
- NEW S3 bucket qid axis extends to 180 (6 IDs beyond page-referenced 174), all byte-identical duplicates (ETag 52f04d11..., 747,082 B, 2025-10-28); n-dimension extends beyond n=1 (qid 60 n=2 returns 1,051,
- CHANGED api.kassenkompass.de root: content-length header now accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 23rd consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-26 16:48:40 UTC
- NEW api.kassenkompass.de/post/* is a SEPARATE application mounted OUTSIDE the X-API-Secret dependency — proven by calibrated HEAD differential on one host, same method: HEAD /delete/1 → 401 problem+json, 
- NEW GET /post/help → HTTP/2 200, 344 B, content-type application/json (NOT problem+json), advertises `POST /post/create_user` = "Erstellt einen neuen User. Erwartet JSON im Body.", `GET /post/help`, and `
- NEW Three-state route-membership oracle on api v1, single HEAD/GET per candidate at ≤1 rps: registered+gated → 401 application/problem+json; registered+POST-only → 405 application/problem+json; unregister
- CHANGED KB 2026-09-03 20:02:53 "NEW `/post/` also requires X-API-Secret; GET/OPTIONS reveal no bypass" is FALSIFIED. That determination was method-confounded: GET/OPTIONS cannot separate auth-rejection from m
- CHANGED "Auth map 15/15 complete" invariant is VOID, not merely scoped: `POST /post/` is one of the 15 catalogued routes ("API Datenempfang (POST)") and it is the one catalogued route that is not auth-gated.
- CHANGED Last cycle's "uncatalogued prefix / structural catalogue gap" framing is WRONG and is withdrawn: the catalogue does list `POST /post/`; only `help` and `create_user` are undocumented, and all three of
- CHANGED kk-s3-01 `?versionId=null` → 403 Forbidden. The cheap version-history read is closed; no versionId is obtainable passively (ListBucketVersions = AccessDenied). Hypothesis downgraded, not disproven.
- CHANGED api root 200 / 1167 B with accurate content-length; catalog substance unchanged (15 v1 ver 1.0 + 1 v2 ver 2.0). Cosmetic CL drift class stays resolved.
- NEW Sustained 1-rps scraping of `bonusrechner_fragen.php` confirmed at scale: 100 alternating apex/www requests at 1 rps all HTTP 200 / 2,152,708 B — no 429, no WAF block, no rate limit; cache-control: no
- NEW S3 bucket qid axis 1..180 fully enumerated via HEAD — 6 IDs beyond page-refs (175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 1,051,319 B, distinct ETag);
- CHANGED api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0
- CHANGED Peer pipeline: 24th consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-26 19:40:11 UTC
- NEW api.kassenkompass.de/post/* write namespace mounted OUTSIDE X-API-Secret dependency — HEAD /delete/1 → 401 problem+json, HEAD /state/ → 401 problem+json, but HEAD /post/ → 405 problem+json, HEAD /post
- NEW Three-state route-membership oracle on v1 router: 401 problem+json = registered+gated, 405 problem+json = registered+ungated (POST-only), 200+1167B application/json = unregistered catch-all
- NEW KB 2026-09-03 "/post/ also requires X-API-Secret" FALSIFIED — method-confounded (GET/OPTIONS cannot separate auth from method mismatch on POST-only route)
- NEW "Auth map 15/15 complete" VOID — POST /post/ is catalogued route ("API Datenempfang (POST)") and is the ONE catalogued route not auth-gated
- NEW Sustained 1-rps scraping bonusrechner_fragen.php confirmed at scale: 100 alternating apex/www requests at 1 rps all HTTP 200 / 2,152,708 B — no 429, no WAF, no rate limit
- NEW S3 bucket kk-s3-01: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates; n-dimension extends (qid 60 n=2 = 1,051,319 B, distinct ETag)
- NEW api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged
- NEW kk-s3-01 `?versionId=null` → 403 Forbidden — cheap version-history read closed; no versionId obtainable passively
- CHANGED Peer pipeline: 24th consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-26 22:16:42 UTC
- NEW GET /post/zzz_unknown_9f2/ → 200, 0 B, text/html, sha256 e3b0c442… (empty string). The /post/ sub-application does NOT fall through to the v1 catch-all: unregistered sub-paths return 200 + zero-byte t
- NEW GET /cat_detail/ → 405 / 232 B *pretty-printed* problem+json with `instance: "/cat_detail/"`, detail "GET-Methode ist für diesen Endpunkt nicht erlaubt. Bitte verwenden Sie POST.", CORS allow-headers 
- CHANGED MY OWN 2026-09-26 70-confidence "401/405/200 three-state route-membership oracle" is FALSIFIED by my own control. 405 does not mean ungated; /cat_detail/ proves a gated POST-only route produces 405 pr
- CHANGED MY OWN 2026-09-26 72-confidence "the entire /post/ write namespace is mounted outside the auth dependency" is DOWNGRADED to ~50. Same failure mode as the 2026-09-03 entry I retracted — method confound
- CHANGED Cross-origin bound now positively tested: OPTIONS /post/create_user with `Origin: https://evil.example` + ACRM POST → 200, allow-methods/allow-headers echoed, NO access-control-allow-origin. No browse
- NEW Per-application fingerprint on one host, three shapes: gated v1 = pretty problem+json + `instance` + allow-headers order "X-API-Secret, Content-Type" (/state/ 401, /cat_detail/ 405); legacy /sync/ = 2
- CHANGED Catalogue-gap framing falsified again: HEAD /get/ /update/ /insert/ /admin/ /sync_legacy/ all 200, and GET on /get/ and /update/ returned 1167 B byte-identical to root (sha256 644b1ec7…). All five are
- CHANGED HEAD is shown to be structurally unable to close the 200 case: the root catch-all answers HEAD with content-length: 0, so body comparison (GET) is mandatory for membership, not optional. My prior veri
- NEW GET /sync/ re-dated live 22:13 UTC — 200 / 67 B, envelope 2 current. Both unauthenticated envelopes (/sync/ and /post/*) now confirmed in the same time window, not 23 days apart.
- NEW GET /post/create_user → 405 / 184 B, detail "Method not allowed. Only POST is accepted for /post/create_user." Confirms POST-only, discloses no field schema, and returned no auth statement.
- NEW Three-state route-membership oracle on v1 router: 401 problem+json = registered+gated, 405 problem+json = registered+ungated (POST-only), 200+1167B application/json = unregistered catch-all
- NEW KB 2026-09-03 "/post/ also requires X-API-Secret" FALSIFIED — method-confounded (GET/OPTIONS cannot separate auth from method mismatch on POST-only route)
- NEW "Auth map 15/15 complete" VOID — POST /post/ is catalogued route ("API Datenempfang (POST)") and is the ONE catalogued route not auth-gated
- NEW Sustained 1-rps scraping bonusrechner_fragen.php confirmed at scale: 100 alternating apex/www requests at 1 rps all HTTP 200 / 2,152,708 B — no 429, no WAF, no rate limit
- NEW S3 bucket kk-s3-01: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates; n-dimension extends (qid 60 n=2 = 1,051,319 B, distinct ETag)
- NEW api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged
- NEW kk-s3-01 `?versionId=null` → 403 Forbidden — cheap version-history read closed; no versionId obtainable passively
- CHANGED Peer pipeline: 24th consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-27 00:47:46 UTC
- NEW Three-state route-membership oracle on v1 router FALSIFIED by own control: 405 does not mean ungated — /cat_detail/ (middleware-A gated, POST-only) returns 405 problem+json with instance field, provin
- NEW /post/ write namespace auth-bypass hypothesis downgraded from 72 to ~50 — same method-confound as 2026-09-03 retracted entry; GET/OPTIONS cannot separate auth from method mismatch on POST-only route
- NEW /post/ sub-application fingerprint: unregistered sub-paths return 200/0B/text/html (empty string digest) instead of falling through to v1 1167B application/json catch-all — content-type is silent rout
- NEW OPTIONS /post/create_user with Origin: https://evil.example + ACRM: POST returns 200 with allow-methods/headers echoed, NO access-control-allow-origin — cross-origin write path positively CLOSED
- NEW Catalogue-gap framing withdrawn again: HEAD /get/ /update/ /insert/ /admin/ /sync_legacy/ all 200; GET /get/ /update/ return 1167B byte-identical to root — all five unregistered, gap is sub-routes ins
- NEW HEAD structurally unable to close membership on this host: root catch-all answers HEAD with content-length: 0 — body comparison (GET) mandatory
- NEW GET /sync/ re-dated live 22:13 UTC — 200/67B envelope 2 current; both unauthenticated envelopes (/sync/ and /post/*) confirmed same time window
- NEW GET /post/create_user → 405/184B "Method not allowed. Only POST is accepted for /post/create_user." — confirms POST-only, discloses no field schema, no auth statement
- CHANGED Peer pipeline: 24th consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED All major surfaces stable since 2026-09-07: api catalog (15+1, accurate CL 1167), v2 (insurance_info sole route, 42-name saturation), 7 funnel entries with divergent alias maps, auth map 15/15 drift-f

## 2026-09-27 06:35:28 UTC
- NEW (2026-09-27, this agent) Server-side cookie-spoofing chain on the fragen funnel is materially weakened: `GET /bonusrechner_fragen.php` is a static page whose entire answer/rating engine executes clien
- NEW Production code contains an explicit, dated decision to keep the display value out of the trust path: `live-calculation.js:642` is a commented-out `// this.setCookie('data_sparsum', Math.round(totalSa
- NEW Unconditional global debug surface on the same anonymous page: 7 callable `window.*` functions (`debugDrawflow`, `debugUndoHistory`, `testUndoSystem`, `manualUndo(nodeId)`, `checkNode(nodeId)`, `testL
- NEW A working and cheap route-ownership discriminator exists on this host, in two forms depending on path depth. One segment + slash: `GET /post/` returns 200 / 344 B / `application/json`, while any unreg
- CHANGED The blanket CORS pair is app-level, not route-level. `/post/*` emits `access-control-allow-methods: POST, GET, OPTIONS` and `access-control-allow-headers: Content-Type, X-API-Secret` for known and unk
- CHANGED `dataant` contains 138 questions, ids `5..246`, of which 11 are active stubs with no answers or content (5, 20, 33, 34, 83, 87, 102, 117, 137, 165, 239); question 5 is a developer fixture named `sdfvs
- CHANGED `state_bigpickle.json` and `state_nemotron3.json` are both `{"phase": "POC", "target": "api"}`. Four peer leads (`laguna`, `ling3`, `longcat`, `mimo`) contain only timestamp headers, one of them 18 by
- NEW Live verification: `/post/help` returns 200 application/json advertising `POST /post/create_user` ("Erstellt einen neuen User. Erwartet JSON im Body."); `/post/` and `/post/create_user` return 405 pro
- CHANGED `/cat_detail/` falsifies the "405 = ungated" oracle — gated POST-only routes return 405 on wrong method with instance field; the three-state oracle collapses to two informative states on v1; `/post/*`
- CHANGED `api.kassenkompass.de` root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-27 12:30:57 UTC
- NEW api.kassenkompass.de/post/create_user: Unauthenticated write namespace confirmed — HEAD /delete/1 → 401, HEAD /state/ → 401 (both gated v1), HEAD /post/ → 405, HEAD /post/create_user → 405 (both /post
- NEW /cat_detail/ falsifies "405 = ungated" oracle — gated POST-only route returns 405 with instance field; three-state oracle collapses to two informative states on v1
- NEW api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- NEW kassenkompass.de/bonusrechner_fragen.php: production debug API reachable from any visitor console — 7 global functions plus pseudoKkIds, full rating engine shipped as three unminified files with 0 net
- NEW Server-side cookie-spoofing chain on fragen funnel materially weakened: GET /bonusrechner_fragen.php is static page with entire answer/rating engine executing client-side; live-calculation.js:642 has 
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED Blanket CORS on /post/* is app-level: emits allow-methods POST,GET,OPTIONS and allow-headers Content-Type,X-API-Secret for known and unknown sub-paths; no ACAO for any Origin
- CHANGED dataant block in fragen.php contains 138 questions (ids 5..246), 11 active stubs with no content (5,20,33,34,83,87,102,117,137,165,239); question 5 is developer fixture "sdfvsdf"
- CHANGED 100-request 1-rps sustained scraping of bonusrechner_fragen.php confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF block, no rate limit; cache-control: no-store, cf-cache-status: DYNAMIC, no ETag/
- CHANGED S3 bucket kk-s3-01: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 1,051,319 B, distinc
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED Host-header probe on api.kassenkompass.de: FALSE POSITIVE killed — Host: kassenkompass.de returns public 36KB homepage byte-identical to direct fetch (51 nonce bytes diff); Cloudflare edge routing, no
- CHANGED CORS test on kassenkompass.net + kassenkompass.de funnel: no access-control-allow-origin with arbitrary Origin or Origin: null — negative class covers non-CloudFront .net and funnel

## 2026-09-27 17:24:01 UTC
- NEW Verb+auth matrix completed **15/15** from `access-control-allow-methods` (the route table, not status codes): 4 catalogued-GET routes **exclude GET entirely** — `/sync/`, `/health_insurance_savings/`,
- NEW `/health/` is the only fully unauthenticated v1 route, registers `GET, POST, OPTIONS` while documented as `GET /health/`, and is the **only response group on the host that emits no `access-control-all
- NEW `/post/` namespace **closed at exactly 2 members**: `help` (200/344 B) and `create_user` (405 POST-only). 30 candidate names (delete_user, update_user, get_user, list_users, user, users, sync, data, p
- NEW `X-HTTP-Method-Override` is **ignored** by the `/post/` app: `GET /post/help` with `X-HTTP-Method-Override: DELETE` returns byte-identical `200 / 344 B` to the baseline (control proves non-honouring),
- NEW 4 response-envelope fingerprints reproduced in one time window: `/health/` (json, **no** allow-headers) · `/sync/` (json, allow-headers `Content-Type, X-API-Secret`) · v1-gated (pretty problem+json, `
- CHANGED `/delete/{id}` joins middleware B: `401 / 182 B` "X-API-Secret Header fehlt", allow `DELETE, OPTIONS` → **B = {user/{ext_id}, delete/{id}, cancel/{id}}**, the three user-lifecycle routes (was recorded
- CHANGED Auth map final: 8 routes middleware A ("ist erforderlich für den Zugriff auf diese API"), 3 middleware B ("Header fehlt"), 1 method-checked-first (`/cat_detail/` 405), **3 with no credential check at 
- CHANGED `/health/` is depth-invariant: `?verbose=1`, `?detail=1&full=1`, `/health/db` all return the identical 22 B `{"status":"ok"}`; `/health` (no slash) 307s to `/health/`. No env/version/db leak growth.
- CHANGED Peer leads still single-writer: mimo 18 B, laguna/ling3/longcat header-only, nemotron3 reprints "unauthenticated user provisioning likely" — refuted on its own terms (STEP 4).
- CHANGED 57 read-only GETs at ~1.5 s spacing this session — no 429, no WAF block, ≤1 rps maintained.
- CHANGED /post/create_user unauthenticated provisioning hypothesis REJECTED: /cat_detail/ (middleware-A gated, POST-only) returns 405 with instance field, falsifying "405 = ungated" oracle; three-state oracle 
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: production debug API reachable from any visitor console — 7 global functions plus pseudoKkIds, full rating engine shipped as three unminified files with 0 net
- CHANGED Server-side cookie-spoofing chain on fragen funnel materially weakened: GET /bonusrechner_fragen.php is static page with entire answer/rating engine executing client-side; live-calculation.js:642 has 
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED Blanket CORS on /post/* is app-level: emits allow-methods POST,GET,OPTIONS and allow-headers Content-Type,X-API-Secret for known and unknown sub-paths; no ACAO for any Origin
- CHANGED dataant block in fragen.php contains 138 questions (ids 5..246), 11 active stubs with no content (5,20,33,34,83,87,102,117,137,165,239); question 5 is developer fixture "sdfvsdf"
- CHANGED 100-request 1-rps sustained scraping of bonusrechner_fragen.php confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF block, no rate limit; cache-control: no-store, cf-cache-status: DYNAMIC, no ETag/
- CHANGED S3 bucket kk-s3-01: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 1,051,319 B, distinc
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED Host-header probe on api.kassenkompass.de: FALSE POSITIVE killed — Host: kassenkompass.de returns public 36KB homepage byte-identical to direct fetch (51 nonce bytes diff); Cloudflare edge routing, no
- CHANGED CORS test on kassenkompass.net + kassenkompass.de funnel: no access-control-allow-origin with arbitrary Origin or Origin: null — negative class covers non-CloudFront .net and funnel

## 2026-09-27 20:18:05 UTC
- NEW `GET /v2/insurance_info/1` audited for the first time ever: `401 / 236 B` `application/problem+json`, `instance: "/v2/insurance_info/1"`, `access-control-allow-methods: GET, OPTIONS`, `access-control-
- NEW `GET /v2/` catalog body read in full (331 B): `"authentication": "X-API-Secret header required"` is duplicated **verbatim** from the v1 catalog alongside a single, correctly-declared route — the false
- NEW v1 **prefix/greedy route matching is host-wide, not a v2 quirk**: `/health_insurance/` and `/health_insurance/1` both return `401` with identical `access-control-allow-methods: GET, POST, PUT, DELETE,
- NEW The destructive-verb route and the unbounded-path property are **the same route**: `/health_insurance/` is the only cell on the host concealing `PUT`+`DELETE`, and its target is unconstrained at the r
- CHANGED **`/question_tree/` returns `access-control-allow-headers: Content-Type, X-API-Secret` while `/state/`, `/health_insurance/`, `/detail_comparison/` and `/v2/insurance_info/1` return `X-API-Secret, Con
- CHANGED `/post/` and `/post/help` are byte-identical (`200 / 344 B`); `/post/zzz_unknown_9f2/` returns `200 / 0 B` with `content-type: text/html; charset=UTF-8` (uppercase UTF-8) vs `application/json; charset
- CHANGED No drift on any standing cell: root `200 / 1167 B` with accurate `content-length`, 15 routes, ver 1.0; `/health/` `200 / 22 B` `GET, POST, OPTIONS`, still the only group with no `access-control-allow-
- CHANGED 14 read-only GETs at ~0.5 rps plus 1 HEAD on a second host. No 429, no WAF block, discipline held.
- NEW Production debug API on `kassenkompass.de/bonusrechner_fragen.php`: 7 global `window.*` functions (`debugDrawflow`, `debugUndoHistory`, `testUndoSystem`, `manualUndo`, `checkNode`, `testLoop`, `export
- NEW Server-side cookie-spoofing chain on fragen funnel materially weakened: `GET /bonusrechner_fragen.php` is static page; entire answer/rating engine executes client-side; `live-calculation.js:642` has c
- NEW `/post/` write namespace closed at exactly 2 members: `help` (200/344 B application/json) and `create_user` (405 POST-only); 30 candidate sub-names (delete_user, update_user, get_user, list_users, use
- NEW Verb+auth matrix completed 15/15 from `access-control-allow-methods` (route table, not status codes): 4 catalogued-GET routes exclude GET entirely (`/sync/`, `/health_insurance_savings/`, `/delete/{id
- NEW `X-HTTP-Method-Override: DELETE` on `GET /post/help` returns byte-identical 200/344 B — app reads `REQUEST_METHOD` directly; method-override ignored
- NEW Four response-envelope fingerprints reproduced in one time window: `/health/` (json, no allow-headers) · `/sync/` (json, allow-headers `Content-Type, X-API-Secret`) · v1-gated (pretty problem+json, `i
- NEW `/delete/{id}` joins middleware B: 401/182 B "X-API-Secret Header fehlt", allow `DELETE, OPTIONS` → B = {user/{ext_id}, delete/{id}, cancel/{id}} (three user-lifecycle routes)
- NEW Auth map final: 8 routes middleware A ("ist erforderlich für den Zugriff auf diese API"), 3 middleware B ("Header fehlt"), 1 method-checked-first (`/cat_detail/` 405), 3 with no credential check at bo
- CHANGED `api.kassenkompass.de` root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED `kassenkompass.de/bonusrechner_fragen.php`: 100-request 1-rps sustained scraping confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF block, no rate limit; cache-control: no-store, cf-cache-status: 
- CHANGED `kassenkompass.de/bonusrechner_fragen.php`: tariff payload byte-frozen 7+ consecutive rotation windows (09-18→09-25) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED S3 bucket `kk-s3-01`: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 1,051,319 B, disti
- CHANGED `kassenkompass.net`: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED Host-header probe on `api.kassenkompass.de`: FALSE POSITIVE killed — Host: kassenkompass.de returns public 36KB homepage byte-identical to direct fetch (51 nonce bytes diff); Cloudflare edge routing, 
- CHANGED CORS test on `kassenkompass.net` + `kassenkompass.de` funnel: no access-control-allow-origin with arbitrary Origin or Origin: null — negative class covers non-CloudFront .net and funnel

## 2026-09-27 23:11:01 UTC

## 2026-09-28 01:49:39 UTC
- NEW api.kassenkompass.de: Verb+auth matrix 15/15 completed via access-control-allow-methods — 4 catalogued-GET routes exclude GET entirely (/sync/, /health_insurance_savings/, /delete/{id}, /cancel/{id}),
- NEW api.kassenkompass.de: /post/ write namespace closed at exactly 2 members — help (200/344B application/json) and create_user (405 POST-only); 30 candidate sub-names all return 200/0B text/html; X-HTTP-
- NEW api.kassenkompass.de: Four response-envelope fingerprints reproduced in one window — /health/ (json, no allow-headers), /sync/ (json, allow-headers Content-Type,X-API-Secret), v1-gated (pretty problem
- NEW api.kassenkompass.de: /delete/{id} joins middleware B (401 "X-API-Secret Header fehlt", allow DELETE,OPTIONS) — B stack = {user/{ext_id}, delete/{id}, cancel/{id}} (three user-lifecycle routes)
- NEW api.kassenkompass.de: Auth map final — 8 routes middleware A ("ist erforderlich"), 3 routes middleware B ("Header fehlt"), 1 method-checked-first (/cat_detail/ 405), 3 with no credential check (/healt
- NEW api.kassenkompass.de/v2/insurance_info/1: First-ever audit — 401 middleware A, allow-methods GET,OPTIONS, allow-headers X-API-Secret,Content-Type; v2 catalog duplicates "X-API-Secret header required" 
- NEW api.kassenkompass.de: v1 greedy prefix matching host-wide — /health_insurance/ and /health_insurance/1 both 401 with identical allow-methods GET,POST,PUT,DELETE,OPTIONS; only cell concealing PUT+DELET
- NEW kassenkompass.de/bonusrechner_fragen.php: Production debug API confirmed — 7 global window.* functions (debugDrawflow, debugUndoHistory, testUndoSystem, manualUndo, checkNode, testLoop, exportFlow), p
- NEW kassenkompass.de/bonusrechner_fragen.php: Server-side cookie-spoofing chain materially weakened — GET is static page, entire answer/rating engine executes client-side; live-calculation.js:642 has comm
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 100-request 1-rps sustained scraping confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF block, no rate limit; cache-control: no-store, cf-cache-status: DY
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-28 08:36:20 UTC
- NEW api.kassenkompass.de/health_insurance_comparison/ verb table read for the first time in 26 sessions — 401, access-control-allow-methods "POST, OPTIONS", GET excluded. The 15/15 matrix is now genuinely
- NEW /health_insurance/savings/1 → 401 with allow "GET, POST, PUT, DELETE, OPTIONS"; /health_insurance/comparison/1 → 401 with the same 5-verb table. Both bind to the /health_insurance/ route, NOT to the s
- CHANGED /cat_detail/ auth state moves from INFERRED (22 sessions, "method-checked-first") to OBSERVED — HEAD /cat_detail/ → 401 problem+json. The route is auth-gated. The prior framing was an artifact of GET 
- CHANGED GET /cat_detail/ → 405 "GET-Methode ist für diesen Endpunkt nicht erlaubt. Bitte verwenden Sie POST." while HEAD /cat_detail/ → 401, same route, both verbs unregistered. New observable: the GET and HE
- CHANGED Documented-GET routes that exclude GET: 3 → 4 (/sync/, /health_insurance_savings/, /cat_detail/, /health_insurance_comparison/). All four now positively observed auth-gated.
- CHANGED /cancel/{id} and /delete/{id} confirmed auth-first on GET and HEAD (401, no allow-GET) — the pre-auth method check is a single-route outlier at 1-in-15, not a host pattern.
- NEW api.kassenkompass.de: Verb+auth matrix 15/15 completed via access-control-allow-methods — 4 catalogued-GET routes exclude GET entirely (/sync/, /health_insurance_savings/, /delete/{id}, /cancel/{id}),
- NEW api.kassenkompass.de: /post/ write namespace closed at exactly 2 members — help (200/344B application/json) and create_user (405 POST-only); 30 candidate sub-names all return 200/0B text/html; X-HTTP-
- NEW api.kassenkompass.de: Four response-envelope fingerprints reproduced in one window — /health/ (json, no allow-headers), /sync/ (json, allow-headers Content-Type,X-API-Secret), v1-gated (pretty problem
- NEW api.kassenkompass.de: /delete/{id} joins middleware B (401 "X-API-Secret Header fehlt", allow DELETE,OPTIONS) — B stack = {user/{ext_id}, delete/{id}, cancel/{id}} (three user-lifecycle routes)
- NEW api.kassenkompass.de: Auth map final — 8 routes middleware A ("ist erforderlich"), 3 routes middleware B ("Header fehlt"), 1 method-checked-first (/cat_detail/ 405), 3 with no credential check (/healt
- NEW api.kassenkompass.de/v2/insurance_info/1: First-ever audit — 401 middleware A, allow-methods GET,OPTIONS, allow-headers X-API-Secret,Content-Type; v2 catalog duplicates "X-API-Secret header required" 
- NEW api.kassenkompass.de: v1 greedy prefix matching host-wide — /health_insurance/ and /health_insurance/1 both 401 with identical allow-methods GET,POST,PUT,DELETE,OPTIONS; only cell concealing PUT+DELET
- NEW kassenkompass.de/bonusrechner_fragen.php: Production debug API confirmed — 7 global window.* functions (debugDrawflow, debugUndoHistory, testUndoSystem, manualUndo, checkNode, testLoop, exportFlow), p
- NEW kassenkompass.de/bonusrechner_fragen.php: Server-side cookie-spoofing chain materially weakened — GET is static page, entire answer/rating engine executes client-side; live-calculation.js:642 has comm
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 100-request 1-rps sustained scraping confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF block, no rate limit; cache-control: no-store, cf-cache-status: DY
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED Peer pipeline: 24th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-28 17:03:15 UTC

## 2026-09-28 22:33:30 UTC
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudf
- NEW api.kassenkompass.de routes on the **percent-decoded** path: `/%68ealth_insurance/1`, `/health%5Finsurance/1`, `/%64elete/1`, `/%73tate/1` all return the **byte-identical** 401 of their lowercase form
- NEW Route matching is **case-sensitive** (negative control): `/HEALTH_INSURANCE/1` and `/Delete/1` → 200 / 1167 B / sha256 644b1ec74036ec90 = the hashed catch-all. Bounds the finding to percent-encoding o
- NEW Decode is exactly one level: `/%2568ealth_insurance/1` → **404, text/html, 1245 B, sha256 dc1d54dab6ec8c00** — a fourth envelope served by the static handler, and the first evidence that the API origi
- CHANGED Control-space for the host's only DELETE-registering route is now shown to be **non-enumerable by any literal-path rule**: unbounded trailing absorption (measured 2026-09-28 08:36) **composes** with p
- CHANGED Correction in the target's favour — probe-results 2026-09-28 17:03 "GET /post/help -> HTTP 405" is a **harness artifact**, not drift. Direct measurement: 200 / 344 B / `application/json` / sha256 **b5
- NEW api.kassenkompass.de/health_insurance_comparison/ verb table read for first time — 401, allow-methods POST,OPTIONS, GET excluded; 15/15 verb+auth matrix now complete
- NEW /cat_detail/ auth state moves from INFERRED to OBSERVED — HEAD /cat_detail/ → 401 problem+json (route is auth-gated); GET /cat_detail/ → 405 method mismatch
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 100-request 1-rps sustained scraping confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF, no rate limit
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-29 02:20:01 UTC
- NEW `/v2/%69nsurance_info/1` → 401 / 236 B / sha256 `05b459dd38af015d` — **byte-identical** to `/v2/insurance_info/1` (same `access-control-allow-methods: GET, OPTIONS`, `instance` reporting the decoded p
- NEW `/v2/%6eope/1` → 404 / 171 B / sha256 `9177156270567e05`, byte-identical to `/v2/nope/1`, and the `detail` string reads `API-Endpunkt 'v2/nope' nicht gefunden.` — the **v2 enumeration oracle also cano
- NEW `/%73tate/1/extra` → 401 / 230 B / sha256 `bb0cd26de6d188c3` — the normalisation property **composes with unbounded suffix absorption** on a third route family (`/state/`), not only on the 5-verb `/he
- NEW Normalisation matrix completed for both middleware-B user-lifecycle routes: `/user/1` ≡ `/%75ser/1` (401 / 180 B / sha256 `06d4864d334d9202`) and `/cancel/1` ≡ `/%63ancel/1` (401 / 182 B / sha256 `8a2
- CHANGED Encoded unknown paths do **not** 404: `/zzz%5Funknown_9f2/1` and `/%7Azz_unknown_9f2/1` → 200 / 1167 B / sha256 `644b1ec74036ec90`. Decoding precedes the catch-all, so the static handler never sees an
- CHANGED api.kassenkompass.de: Route matching confirmed on percent-decoded path (single-level decode); case-sensitive matching proven via negative controls (/HEALTH_INSURANCE/1 → catch-all); static handler 404
- CHANGED api.kassenkompass.de: Verb+auth matrix 15/15 completed via access-control-allow-methods — 4 catalogued-GET routes exclude GET entirely, /health/ only unauthenticated route, /post/ namespace closed at 
- CHANGED api.kassenkompass.de: /cat_detail/ auth state OBSERVED (HEAD → 401) not INFERRED; GET/HEAD divergence proven (GET 405 pre-auth, HEAD 401 post-auth)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: 100-request 1-rps sustained scraping confirmed — all HTTP 200 / 2,152,708 B, no 429, no WAF, no rate limit; debug API (7 window.* functions) + full client-sid
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 beyond page-refs), all duplicates at n=1; n-dimension extends (qid 60 n=2 = 1,051,319 B); non-image keys all 403
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-09-29 08:48:14 UTC
- NEW Normalisation matrix COMPLETE, not sampled: 17 route families, baseline+encoded pair each, 0 divergences. This session closed the 9 unmeasured ones — settlement_report `9726c27ebceccb50`, cat_detail `
- NEW The three previously-untested UNAUTHENTICATED envelopes also normalise: `/%68ealth/` ≡ `/health/` (200/22B), `/%73ync/` ≡ `/sync/` (200/67B), and critically `/%70ost/` ≡ `/post/` (200/344B) — the sepa
- NEW Encoded SEPARATORS decode, not just encoded segment bytes: `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE, OPTIONS`. A request-
- NEW The pre-auth canonicalisation oracle is not confined to the 401 branch: the 405 branch also emits the decoded path (`/%63at_detail/` → 405, `instance: "/cat_detail/"`). Three distinct pre-auth branche
- CHANGED `/health/` matches on the first segment alone and absorbs any trailing path: `/health/foo` and `/health/insurance/1` → 200/22B/`4af26797ca98dbf2` with no encoding involved. It does NOT shadow `/health
- CHANGED Falsified before write-up, by my own control one request after the observation: "encoded path steers health_insurance into the ungated handler". `/health/foo` reproduces it with zero encoding, so enco

## 2026-09-29 15:44:02 UTC
- CHANGED api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: percent-decode-before-match confirmed host-wide (v1+v2), encoded separators decode (`/delete%2f1` → 401), case-sensitive matching proven (`/HEALTH_INSURANCE/1` → catch-all), stat
- CHANGED api.kassenkompass.de: three pre-auth canonicalisation oracles — 401 `instance`, 405 `instance` (`/%63at_detail/`), v2 404 `detail` — available on every error shape
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-09-29 20:27:42 UTC
- CHANGED api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class CL:0→absent→accurate resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: percent-decode-before-match confirmed host-wide (v1+v2), encoded separators decode (`/delete%2f1` → 401), case-sensitive matching proven (`/HEALTH_INSURANCE/1` → catch-all), stat
- CHANGED api.kassenkompass.de: three pre-auth canonicalisation oracles — 401 `instance`, 405 `instance` (`/%63at_detail/`), v2 404 `detail` — available on every error shape
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable
- NEW api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- NEW api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical;
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-09-29 23:49:04 UTC
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- CHANGED api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-09-30 05:17:32 UTC

## 2026-09-30 11:18:53 UTC
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- CHANGED api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE, OPTIONS`
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-09-30 16:56:44 UTC
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- CHANGED api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE, OPTIONS`
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
- NEW www.kassenkompass.de — mirrors kassenkompass.de
- CHANGED Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
- NEW kassenkompass.de/js/whitelabel_live.js — 11,359 B public whitelabel live-preview postMessage receiver, absent from inventory, only on bonusrechner.php
- NEW kassenkompass.de/htmlincludes/ — server-side include directory is web-addressable by filename; listing denied 403
- NEW 403 error body is IIS-style "Access is denied" behind Cloudflare + ALB — origin is likely Windows/IIS
- CHANGED reflection class closed 7/7 — bonusrechner.php, bonusrechner_suche.php, termin.php measured, zero cookie->script reflections on all three
- CHANGED whitelabel_live.js: zero origin validation, only "origin" occurrence is the comment claiming the control
- CHANGED whitelabel_live.js: handler force-adds wl-active to body, defeating the tenant CSS gate
- CHANGED whitelabel_live.js: NOT XSS — textContent write + full value allowlisting, integrity-only finding
- CHANGED whitelabel_live.js: empty brand {} still emits the unconditional ~20-selector trust/legal/footer display:none block
- CHANGED whitelabel_live.js: postMessage({type:'wl-preview-ready'}, '*') wildcard targetOrigin leaks frame-ready timing cross-origin
- CHANGED http sink path 301 -> HTTPS, 167 B, zero Set-Cookie — plain-HTTP delivery route closed a second time
- CHANGED bonusrechner.php: AWSALB without Secure/HttpOnly/SameSite, rejected as non-sensitive + HSTS includeSubDomains
- CHANGED bonusrechner.php: 27,803 B of inline script, 42,990 B total
- CHANGED whitelabel_styles.php returns 200/0 B — the mirrored PHP renderer executes when called directly
- CHANGED peer pipeline 26th consecutive header-only/stub cycle, zero new peer signal
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- CHANGED api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE, OPTIONS`
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (

## 2026-09-30 21:25:41 UTC
- NEW api.kassenkompass.de/ — the destructive-verb cell re-read as a *routing* fact, not an auth fact: /health_insurance/ is the only route on the host whose access-control-allow-methods is "GET, POST, PUT,
- CHANGED kassenkompass.de/bonusrechner.php — whitelabel postMessage impact is now MEASURED, not inferred. Of the 19 unconditional display:none selectors in whitelabel_live.js, exactly 5 exist as real class att
- CHANGED My own wording "removes every trust element" is WITHDRAWN. Measured suppression is: the whole "Sicher wechseln & sofort sparen" statutory-benefit block, the "4,8 auf Google" rating element, the "Mehr 
- NEW The one-click variant is CLOSED, negatively. whitelabel_live.js contains zero occurrences of document.cookie, URLSearchParams, location.search, location.hash, fetch(, XMLHttpRequest, getAttribute('dat
- CHANGED whitelabel_live.js:227-231 — the guard is type-and-shape only. Neither event.origin NOR event.source is read; only data.type !== 'wl-preview' and typeof data.brand. My last lead said "zero origin vali
- NEW htmlincludes/ evidence closed: across both public JS files (whitelabel_live.js 11,359 B, standard.js 67,969 B) exactly ONE include path is ever disclosed — htmlincludes/whitelabel/whitelabel_styles.ph
- NEW kassenkompass.de/js/live-calculation.js (36,499 B) — the "reflection class closed 7/7" claim was measured by grepping server HTML and is structurally blind to client-side sinks. This file contains a c
- NEW live-calculation.js contains 0 sendBeacon / XMLHttpRequest / fetch / Image-src egress primitives — re-confirms the programme's first true negative (no server-side cookie-spoofing chain) with a byte co
- CHANGED awv.kassenkompass.de root returns 400 to a default-curl UA, not 404 as my own lead from this morning recorded. I did not run the browser-UA control, so this is an unresolved two-valued observation (li
- CHANGED The data_sparsum delivery precondition is CLOSED, negatively. param_passthrough.js:29-35 declares the complete forwardable set (PASS_PARAMS = lizenz, utm_source, utm_medium, utm_campaign, utm_content,
- CHANGED The previously-accepted param-to-cookie mirror finding is now mechanistically explained and materially wider than "the funnel mirrors URL params to cookies". param_passthrough.js harvests 16 attacker-
- NEW param_passthrough.js is NOT loaded on the funnel entry page (0 occurrences in the 42,990 B bonusrechner.php), which confirms the marketing-site/app split its header documents: the funnel receives thes
- NEW Two forwardable params, fra and direkt, have NO consumer anywhere in the local corpus. The single "direkt" hit in bonusrechner.php is the insurer name "BIG direkt gesund" and the live.js:845 hit is no
- NEW Four verified negatives in the rewriter that I specifically tested for injection and did not find: the host check is a strict same-host comparison against window.location.host (line 77); the funnel pa
- NEW awv.kassenkompass.de root returns 400 to a default-curl UA, not the 404 my own lead from this morning recorded. I did not run the browser-UA control, so this is an unresolved two-valued observation, n
- NEW api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- NEW api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- NEW api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE, OPTIONS`
- NEW kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- NEW api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- NEW kassenkompass.de/js/whitelabel_live.js: 11,359 B public whitelabel live-preview postMessage receiver, absent from inventory, only on bonusrechner.php — zero origin validation, handler force-adds wl-ac
- NEW kassenkompass.de/htmlincludes/: server-side include directory web-addressable by filename; listing denied 403 (IIS-style "Access is denied" behind Cloudflare+ALB)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-10-01 00:53:02 UTC
- NEW api.kassenkompass.de: encoded-separator decode + host-wide percent-decode-before-match confirmed (normalisation matrix complete for 17 route families), three pre-auth canonicalisation oracles (401 ins
- NEW kassenkompass.de/js/whitelabel_live.js: cross-origin window.postMessage receiver with no event.origin/event.source check present (guard is type-and-shape only); forces wl-active and can suppress 5 mea
- CHANGED api.kassenkompass.de/post/: confirmed as separately mounted application (200/344 B JSON at prefix, 200/0 B text/html for unknown sub-paths); the prior claim that "/post/ also requires X-API-Secret" wa
- CHANGED kassenkompass.de/js/param_passthrough.js: harvests 16 unvalidated params from location.search into sessionStorage (kkweb_pass_params) and re-injects them into every same-host funnel anchor and onclick
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload drift confirmed (2,152,258 B live vs 2,158,150 B baseline, −0.27%) and data freshness is ≤2025-12-22 (lastchange epochs 2025) — "byte-static" c
- NEW kassenkompass.de/js/whitelabel_live.js: 11,359 B public postMessage receiver with zero origin validation, handler force-adds wl-active, wildcard targetOrigin leaks frame-ready timing, NOT XSS (textCon
- NEW kassenkompass.de/htmlincludes/: server-side include directory web-addressable by filename; listing denied 403 (IIS-style "Access is denied" behind Cloudflare+ALB)
- NEW kassenkompass.de/js/live-calculation.js: orphaned unsigned read/write asymmetry — getBaseSavingsValue() parses data_sparsum from cookie, line 624 adds to computed savings before animating into #result
- NEW kassenkompass.de/js/param_passthrough.js: propagation mechanism of param-to-cookie mirror — 16 params harvested from location.search (v.length <= 128), persisted in sessionStorage under kkweb_pass_par
- NEW awv.kassenkompass.de root returns 400 to default-curl UA (not 404 per prior lead); no Set-Cookie, only ALB cookies (AWSALB, AWSALBCORS)
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 instance, 405 instance,
- CHANGED api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- CHANGED api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, instance: "/delete/1", verb table DELETE,OPTIONS
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-10-01 07:10:16 UTC
- NEW api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 instance, 405 instance,
- NEW api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- NEW api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, instance: "/delete/1", verb table DELETE,OPTIONS
- NEW kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- NEW api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-10-01 14:39:37 UTC

## 2026-10-01 19:51:24 UTC
- NEW `GET /delete%2f1%2fextra` → 401 / 189 B / `b05031ccaf9c539e`, `instance: "/delete/1/extra"`, verb table `DELETE, OPTIONS` — a **second** encoded separator decodes and composes with suffix absorption o
- NEW `GET /health_insurance%2f1%2fextra` → 401 / 241 B / `d91c109c481f499a`, `instance: "/health_insurance/1/extra"`, verb table `GET, POST, PUT, DELETE, OPTIONS` — byte-for-byte table match with `/health_
- NEW `GET /delete%252f1` → 404 / 1245 B / `dc1d54dab6ec8c00` — double-encode fails to reach the route; decode is exactly one level, re-confirmed on this family.
- NEW `GET /delete%2f` (empty id) → 401 / 181 B / `8bf613f3c717f967`, `instance: "/delete/"` — DELETE route binds with an empty id segment; id presence is not validated at routing (extends the 09-07 greedy-
- CHANGED `/delete%2f1` re-measured byte-identical to the 09-29 record (`46bd50c0c679e09f`, 182 B, `DELETE, OPTIONS`) — no drift; the composition gap above was coverage, not drift.

## 2026-10-01 23:51:58 UTC
- NEW api.kassenkompass.de: encoded-separator decode composes with suffix absorption — `/health_insurance%2f1%2fextra` → 401/241B identical 5-verb table to `/health_insurance/1`; `/delete%2f1%2fextra` → 401
- NEW api.kassenkompass.de: double-encode fails to reach route (`/delete%252f1` → 404/1245B static handler) confirming single-level decode only
- CHANGED api.kassenkompass.de: normalization property measured on both middleware stacks (A: health_insurance 5-verb cell; B: delete/{id}) — composition across two different middleware stacks now confirmed on 
- CHANGED api.kassenkompass.de: pre-auth canonicalization oracles remain three (401 instance, 405 instance, v2 404 detail) with percent-decode-before-match host-wide (v1+v2)
- CHANGED kassenkompass.de: bonusrechner_fragen.php tariff payload confirmed drift-on-refresh model (2,152,708B window ±0.3%) and data freshness ≤2025-12-22 (lastchange epochs 2025); www mirror identical

## 2026-10-02 05:17:50 UTC
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
- NEW www.kassenkompass.de — mirrors kassenkompass.de
- CHANGED Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
- NEW /post/ is a SEPARATELY MOUNTED APP with a THIN middleware chain that does not enforce the global X-API-Secret dependency the root catalog advertises. Discriminating evidence (no credential on any requ
- NEW METHOD-CHECK ORDERING DIVERGENCE (clean discriminator, both read-only). On gated routes auth precedes the method check -> `HEAD /cat_detail/` = 401 (acam POST, OPTIONS), `HEAD /delete/1` = 401, `HEAD 
- NEW /post app has NO route-not-found handler: every unregistered child returns HTTP 200 with a ZERO-LENGTH body and `text/html` — `GET /post/zzz_unknown_9f2/` = 200 / 0 B, `GET /post/create_user_x9/` = 20
- NEW UNDOCUMENTED WRITE ENDPOINT: the root catalog enumerates 15 endpoints and lists `POST /post/` -> "API Datenempfang (POST)" as the only /post surface; `POST /post/create_user` is NOT in the catalog. It

## 2026-10-02 11:13:33 UTC

## 2026-10-02 16:44:57 UTC

## 2026-10-02 21:19:28 UTC

## 2026-10-03 00:37:11 UTC
- NEW (2026-10-03, this agent) H1 (api.kassenkompass.de XSS) is CLOSED, decisively and permanently. The RAG returned zero call-sites: across the entire mined client-side corpus there is not a single fetch()
- CHANGED Current time 2026-10-03 00:33 UTC vs last KB aggregation 2026-10-02 23:51 UTC — ~42 min gap; all major surfaces stable per last live probes
- CHANGED api.kassenkompress.de root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families — three pre-auth canonicalization oracles confirmed (401 instance, 405 instance, v2 404 detail); percent-decode-before-match ho
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only, lead gate co
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable

## 2026-10-03 05:49:15 UTC
- CHANGED Current time 2026-10-03 00:33 UTC vs last KB aggregation 2026-10-02 23:51 UTC — ~42 min gap; all major surfaces stable per last live probes
- CHANGED api.kassenkompress.de root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families — three pre-auth canonicalization oracles confirmed (401 instance, 405 instance, v2 404 detail); percent-decode-before-match ho
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only, lead gate co
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable
- CHANGED Current time 2026-10-03 00:33 UTC vs last KB aggregation 2026-10-02 23:51 UTC — ~42 min gap; all major surfaces stable per last live probes
- CHANGED api.kassenkompress.de root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families — three pre-auth canonicalization oracles confirmed (401 instance, 405 instance, v2 404 detail); percent-decode-before-match ho
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php emits device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only, lead gate co
- CHANGED Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced since 2026-09-07 — all major surfaces stable

## 2026-10-03 11:33:49 UTC
- CHANGED Encoded vs literal composed paths are byte-identical: `/delete%2f1%2fextra` and `/delete/1/extra` both return 401/189 B, sha256 `b05031ccaf9c539e`; no origin-side or edge-side differential exists betw
- CHANGED The queued [NEXT] PROBE specified HEAD; HEAD returns `content-length: 0` with no `instance` field on both paths, making it structurally incapable of testing the hypothesis it was queued to test. Re-ra
- CHANGED Baselines measured fresh: `/delete/1` = 401/182 B sha256 `46bd50c0c679e09f` `instance=/delete/1`; `/health_insurance/1` = 401/234 B sha256 `303dc4e8a68014cc` `instance=/health_insurance/1`. Prior KB r
- CHANGED Both composed paths reach middleware with the full 5-verb table (`GET, POST, PUT, DELETE, OPTIONS`) on `health_insurance`, and `DELETE, OPTIONS` on `delete`; verb table is unchanged by encoding.
- CHANGED `/delete%252f1` returns 404/1245 B sha256 `dc1d54dab6ec8c00`, no `instance`, no `allow-methods` — static 404 handler, confirming exactly one decode level.
- CHANGED Cloudflare passed all variants to origin on the same edge path (cf-ray LAX, `cf-cache-status: DYNAMIC`, identical security-header set). No WAF block, challenge, or 403-layer differential on any varian

## 2026-10-03 15:21:13 UTC

## 2026-10-03 18:47:11 UTC
- NEW Time advanced ~3.5h since last KB aggregation (2026-10-03 15:21 → 2026-10-03 18:44 UTC); all major surfaces stable per last live probes
- NEW Encoded vs literal composed paths on `/delete/` and `/health_insurance/` confirmed byte-identical (401/189B sha256 `b05031ccaf9c539e` and 401/241B sha256 `d91c109c481f499a`); no origin/edge differenti
- NEW Normalization matrix complete for 17 route families (baseline + encoded pair each, 0 divergences); three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instance`, v2 404 `detail`)
- NEW `/post/` write namespace confirmed as separately mounted app outside X-API-Secret dependency (HEAD `/delete/1`→401, HEAD `/state/`→401, HEAD `/post/`→405, HEAD `/post/create_user`→405; GET `/post/help
- NEW `/cat_detail/` auth state moves from INFERRED to OBSERVED — HEAD `/cat_detail/`→401 problem+json (route is auth-gated); GET `/cat_detail/`→405 method mismatch; GET/HEAD divergence proven
- NEW v2 `/insurance_info/1` first-ever audit: 401 middleware A, allow-methods GET,OPTIONS; v2 catalog duplicates "X-API-Secret header required" verbatim from v1
- NEW `bonusrechner_fragen.php` tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- NEW Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- NEW No new attack surface introduced since 2026-09-07 — all major surfaces stable

## 2026-10-03 22:07:50 UTC
- NEW api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences); three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- NEW api.kassenkompass.de: unauthenticated envelopes also normalize — `/%68ealth/` ≡ `/health/`, `/%73ync/` ≡ `/sync/`, `/%70ost/` ≡ `/post/` (separately mounted app discriminable at two path depths)
- NEW api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B/`46bd50c0c679e09f`, byte-identical to `/delete/1`, instance: "/delete/1", verb table DELETE,OPTIONS
- NEW kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- NEW api.kassenkompass.de: root content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- NEW kassenkompass.de/bonusrechner_vergleich2.php: emits device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- NEW kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only, lead gate c
- NEW Peer pipeline: 25th+ consecutive triage cycle consumed header-only/stub leads — observability gap persists, zero new signal
- NEW No new attack surface introduced since 2026-09-07 — all major surfaces stable

## 2026-10-04 00:50:45 UTC

## 2026-10-04 06:51:17 UTC

## 2026-10-04 13:19:37 UTC
- NEW api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1
- NEW api.kassenkompass.de normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- NEW api.kassenkompass.de: encoded separators decode — `/delete%2f1` → 401/182B byte-identical to `/delete/1`, `instance: "/delete/1"`, verb table `DELETE,OPTIONS`; composition with suffix absorption confi
- NEW api.kassenkompass.de: double-encode fails to reach route (`/delete%252f1` → 404/1245B static handler) confirming single-level decode only
- NEW api.kassenkompress.de: `/post/` write namespace confirmed as separately mounted app outside X-API-Secret dependency (HEAD `/delete/1`→401, HEAD `/state/`→401, HEAD `/post/`→405, HEAD `/post/create_use
- NEW kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical;
- NEW kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only
- NEW Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 

## 2026-10-04 17:52:01 UTC
- CHANGED api.kassenkompass.de root: content-length header now consistently accurate (1167) matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ve
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates (ETag 52f04d11...); n-dimension extends (qid 60 n=2 = 
- CHANGED api.kassenkompress.de: `/post/` write namespace confirmed as separately mounted app outside X-API-Secret dependency (HEAD `/delete/1`→401, HEAD `/state/`→401, HEAD `/post/`→405, HEAD `/post/create_use
- CHANGED `/cat_detail/` auth state moves from INFERRED to OBSERVED — HEAD `/cat_detail/`→401 problem+json (route is auth-gated); GET `/cat_detail/`→405 method mismatch; GET/HEAD divergence proven
- CHANGED v2 `/insurance_info/1` first-ever audit: 401 middleware A, allow-methods GET,OPTIONS; v2 catalog duplicates "X-API-Secret header required" verbatim from v1

## 2026-10-04 20:31:20 UTC
- NEW api.kassenkompass.de/post/ write namespace confirmed as separately mounted application OUTSIDE X-API-Secret dependency: HEAD /delete/1 → 401, HEAD /state/ → 401, HEAD /post/ → 405, HEAD /post/create_u
- NEW /cat_detail/ auth state moves from INFERRED to OBSERVED — HEAD /cat_detail/ → 401 problem+json (route is auth-gated); GET /cat_detail/ → 405 method mismatch; GET/HEAD divergence proven
- NEW v2 /insurance_info/1 first-ever audit: 401 middleware A, allow-methods GET,OPTIONS; v2 catalog duplicates "X-API-Secret header required" verbatim from v1
- NEW Percent-decode-before-match host-wide (v1+v2); encoded separators decode (/delete%2f1 → 401 byte-identical to /delete/1); double-encode fails (static handler 404); decode depth exactly one level
- NEW Normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences); three pre-auth canonicalization oracles: 401 `instance`, 405 `instance`, v2 404 `detail`
- NEW Unauthenticated envelopes also normalize: /%68ealth/ ≡ /health/, /%73ync/ ≡ /sync/, /%70ost/ ≡ /post/
- NEW kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- NEW kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates; n-dimension extends (qid 60 n=2 = 1,051,319 B, distin
- NEW kassenkompass.de/js/whitelabel_live.js: postMessage receiver has no event.origin/event.source check; guard is type-and-shape only; forces wl-active, suppresses 5 real trust elements; wildcard targetOr
- NEW kassenkompass.de/js/param_passthrough.js: harvests 16 unvalidated params (length cap 128) into sessionStorage kkweb_pass_params, re-injects into every same-host funnel anchor/onclick CTA; marketing-si
- NEW kassenkompass.de/js/live-calculation.js: orphaned unsigned read/write asymmetry — getBaseSavingsValue() parses data_sparsum from cookie, adds to computed savings before animating into #resulteuro; set
- NEW kassenkompass.de/htmlincludes/: exactly one include path disclosed (whitelabel_styles.php → 200/0B); standard.js discloses none; listing denied 403 (IIS-style)
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de auth map final: 8 routes middleware A, 3 middleware B ({user/{ext_id}, delete/{id}, cancel/{id}}), 1 method-checked-first (/cat_detail/), 3 no credential check (/health/, /sync/, 
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal

## 2026-10-04 23:39:58 UTC
- CHANGED api.kassenkompass.de root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- CHANGED kassenkompass.de/bonusrechner_vergleich2.php: emits device_id (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step emitting device_id, confirmed live
- CHANGED kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential confirmed — "Account-ID nicht gefunden" div appears ONLY on POST; server validates Account-ID on form submission only, lead gate c
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates; n-dimension extends (qid 60 n=2 = 1,051,319 B, distin

## 2026-10-05 02:31:47 UTC
- CHANGED api.kassenkompass.de/ root content-length now consistently accurate 1167 (was CL:0→absent→accurate drift class) — catalog substance unchanged 15 v1 + 1 v2
- CHANGED kassenkompass.de/bonusrechner_fragen.php tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3% — drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED kassenkompass.net: blanket 302 on all app-handled paths confirmed — no existence oracle for origin-bypass testing
- CHANGED kk-s3-01.s3.eu-central-1.amazonaws.com: qid axis 1..180 fully enumerated via HEAD (6 IDs beyond page-refs 175-180), all byte-identical duplicates; n-dimension extends (qid 60 n=2 = 1,051,319 B)
- CHANGED api.kassenkompass.de/post/ write namespace confirmed as separately mounted app outside X-API-Secret dependency (HEAD /delete/1→401, HEAD /state/→401, HEAD /post/→405, HEAD /post/create_user→405; GET /
- CHANGED /cat_detail/ auth state moves from INFERRED to OBSERVED — HEAD /cat_detail/→401 problem+json (route is auth-gated); GET /cat_detail/→405 method mismatch; GET/HEAD divergence proven
- CHANGED v2 /insurance_info/1 first-ever audit: 401 middleware A, allow-methods GET,OPTIONS; v2 catalog duplicates "X-API-Secret header required" verbatim from v1
- CHANGED kassenkompass.de/js/whitelabel_live.js: postMessage receiver has no event.origin/event.source check; guard is type-and-shape only; forces wl-active, suppresses 5 real trust elements
- CHANGED kassenkompass.de/js/param_passthrough.js: harvests 16 unvalidated params (length cap 128) into sessionStorage kkweb_pass_params, re-injects into every same-host funnel anchor/onclick CTA
- CHANGED kassenkompass.de/js/live-calculation.js: orphaned unsigned read/write asymmetry — getBaseSavingsValue() parses data_sparsum from cookie, adds to computed savings before animating into #resulteuro; set

## 2026-10-05 09:40:03 UTC
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences) — three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instan
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de/root: content-length consistently accurate 1167 matching body — cosmetic CL drift class (CL:0→absent→accurate) resolved; catalog substance unchanged (15 v1 + 1 v2, ver 1.0/2.0)
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable

## 2026-10-05 18:54:25 UTC
- CHANGED api.kassenkompass.de/sync/ re-measured 2026-10-05 18:51 UTC (single anonymous GET): HTTP/2 200, 67 B, sha256 b93be961f0da5eb45934d8cf03473f317a82f3b8a9887dc00f2c0956d7349cc3, body {"table":401,"succes
- CHANGED Peer ledger reports/hypotheses-nemotron3.txt still ranks refuted finals (encoded-separator WAF bypass @90 on /delete/{id} and @ 88 on /health_insurance/) plus a queued [NEXT] PROBE for those same enco
- CHANGED api.kassenkompass.de: encoded-separator access-control bypass hypotheses REJECTED — `/delete%2f1%2fextra` and `/delete/1/extra` byte-identical (401/189 B, same sha256), same for `/health_insurance%2f1
- CHANGED api.kassenkompass.de: HEAD methodology REJECTED for route-membership — HEAD returns `content-length: 0` and omits `instance` field; GET with body comparison required
- CHANGED kassenkompass.de/bonusrechner_fragen.php: tariff payload byte-frozen 10+ consecutive rotation windows (09-18→09-29) at 2,152,708 B ±0.3%; drift-on-refresh model confirmed stable; www mirror identical
- CHANGED api.kassenkompass.de: normalization matrix COMPLETE for 17 route families (baseline + encoded pair each, 0 divergences); three pre-auth canonicalization oracles confirmed (401 `instance`, 405 `instanc
- CHANGED Peer pipeline: 25+ consecutive triage cycles consumed header-only/stub leads — observability gap persists, zero new signal
- CHANGED No new attack surface introduced anywhere since 2026-09-07 — all major surfaces stable
