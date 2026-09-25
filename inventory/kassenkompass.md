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
