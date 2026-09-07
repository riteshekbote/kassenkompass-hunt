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
