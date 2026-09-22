# Hypotheses (ranked)

## RANKED HYPOTHESES 2026-09-02 21:45:31 UTC

## RANKED HYPOTHESES 2026-09-02 23:58:49 UTC

## RANKED HYPOTHESES 2026-09-03 04:13:45 UTC

## RANKED HYPOTHESES 2026-09-03 09:04:36 UTC

## RANKED HYPOTHESES 2026-09-03 13:34:54 UTC

## RANKED HYPOTHESES 2026-09-03 17:32:49 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: IDOR on /user/{ext_id} - cross-user PII access (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/user/1 with no auth header — confirm whether /user/{ext_id} returns data or clean 401 (the sync endpoint returned a stru
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable

## RANKED HYPOTHESES 2026-09-03 20:02:53 UTC
- [70] api.kassenkompass.de: BOLA on /delete/{id} — authenticated arbitrary resource deletion (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: IDOR on /user/{ext_id} - cross-user PII access (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/sync/ -H "X-API-Secret: test" — test if sending any value in X-API-Secret header causes /sync/ to return different data 
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable

## RANKED HYPOTHESES 2026-09-03 22:32:22 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: IDOR on /user/{ext_id} - cross-user PII access (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/user/1 with no auth header — confirm whether /user/{ext_id} returns data or clean 401 (the sync endpoint returned a stru
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root/catch-all discloses full 15-endpoint catalog without auth — least-privilege violation, recon amplifier.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Data endpoints return HTTP 200 + auth-error body instead of 401 — scanner-bypass behavior.
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT.
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins.
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable

## RANKED HYPOTHESES 2026-09-04 00:35:39 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: IDOR on /user/{ext_id} - cross-user PII access (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/settlement_report/9999/13 — read-only, confirm error shape/behavior for financial endpoint under invalid auth (no mutati
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/login — identify OAuth authorize endpoint location and redirect_uri parameter handling (read-only, passive enumeration)
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root/catch-all discloses full 15-endpoint catalog without auth — least-privilege violation, recon amplifier.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Data endpoints return HTTP 200 + auth-error body instead of 401 — scanner-bypass behavior.
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT.
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins.
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret

## RANKED HYPOTHESES 2026-09-04 05:10:14 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- [55] api.kassenkompass.de: Two-tier auth middleware exposes differential authorization paths — BOLA/endpoint-scoping bypass potential (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/login — identify OAuth authorize endpoint location and redirect_uri parameter handling (read-only, passive enumeration)
- NEXT(hypotheses-bigpickle.txt): PROBE: HEAD https://api.kassenkompass.de/ with custom Origin header (e.g. https://evil.com) — confirm CORS policy on root endpoint; also test whether /health/ l
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is authoritative i
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Three distinct auth error paths (RFC 9457 403 message A, RFC 9457 403 message B, HTTP 200 + error body on /sync/) — i
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 in RFC 9457 format — consistent with majority of endpoints, no status-code
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed again this session.
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed.

## RANKED HYPOTHESES 2026-09-04 09:51:41 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Obtain valid X-API-Secret to unlock AUTH_HELPED hypotheses (IDOR /user/{ext_id}, BOLA /settlement_report, two-tier middleware differential test). All pas
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message variant "Ungültiger X-API-Secret" vs other endpoi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ remains sole endpoint returning HTTP 200 + auth error body (known from prior sessions).
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions.
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed.
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT — class not applicable.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is authoritative i
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Three distinct auth error paths (RFC 9457 403 message A, RFC 9457 403 message B, HTTP 200 + error body on /sync/) — i

## RANKED HYPOTHESES 2026-09-04 14:21:08 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message variant "Ungültiger X-API-Secret" vs other endpoi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed

## RANKED HYPOTHESES 2026-09-04 17:44:02 UTC
- [90] api.kassenkompass.de: API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message variant "Ungültiger X-API-Secret" vs other endpoi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed

## RANKED HYPOTHESES 2026-09-04 20:04:27 UTC
- [65] api.kassenkompass.de: Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassen
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed

## RANKED HYPOTHESES 2026-09-04 22:21:25 UTC
- [65] api.kassenkompass.de: Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion (from art/lead_nemotron3.txt)
- [58] api.kassenkompass.de: Draft-Category BOLA via v2 insurance_info wide-variant — unreleased data across all insurers (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: KKX3382745` — rule cross-asset credential reuse against the NEW v2 surfac
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassen
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: REJECTED CORS @ api.kassenkompass.de: no access-control-allow-origin reflection observed on v1 or v2 endpoints — unchanged.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed

## RANKED HYPOTHESES 2026-09-05 00:22:25 UTC
- [58] api.kassenkompass.de: Draft-Category BOLA via v2 insurance_info wide-variant — unreleased data across all insurers (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: KKX3382745` — rule cross-asset credential reuse against the NEW v2 surfac
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassen
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: REJECTED CORS @ api.kassenkompass.de: no access-control-allow-origin reflection observed on v1 or v2 endpoints — unchanged.
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=400 noindex) + load.awv
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom

## RANKED HYPOTHESES 2026-09-05 04:47:18 UTC
- [65] kassenkompass.de: Cookie-stuffing attribution fraud across entire public funnel (from art/lead_bigpickle.txt)
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request a scoped test X-API-Secret + partner-portal account via bugs.olivermaicher.eu — the only open high-value hypotheses (funnel attribution-cookie do
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW — confirm GTM proxy behavior and capture response headers/body; GET https://awv.kassenkompass.de/
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=400 noindex) + load.awv
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely

## RANKED HYPOTHESES 2026-09-05 08:46:09 UTC
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW — confirm GTM proxy behavior and capture response headers/body; GET https://awv.kassenkompass.de/
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=400 noindex) + load.awv
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 12:14:55 UTC
- [70] kassenkompass.de: Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /v2/ exposes a distinct versioned router (v2.0 "breite Variante") with GET /v2/insurance_info/{kk_id} returning draft
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (API-Endpunkt 'v2/X' nicht gefunden) vs v1's full-catalog catch-
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — /v2/insurance_info/{anything} (incl. /1/extra, //1, /1/, %31) all reach the protected ha
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic KKX3382745 is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A (Der bereitgestellte X-API-Secret ist ungültig oder nicht 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 erforderlich; X-A
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 15:32:54 UTC
- [65] kassenkompass.de: Whole-funnel attribution-cookie stuffing → partner commission/lead hijack (from art/lead_bigpickle.txt)
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A (Der bereitgestellte X-API-Secret ist ungültig oder nicht 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 erforderlich; X-A
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 17:47:27 UTC
- [65] kassenkompass.de: Whole-funnel attribution-cookie stuffing → partner commission/lead hijack (from art/lead_bigpickle.txt)
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request a scoped test X-API-Secret + partner-portal account via bugs.olivermaicher.eu — the only open high-value hypotheses (funnel attribution-cookie do
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400.
- LEARN: REJECTED CORS @ api.kassenkompass.de: no access-control-allow-origin reflection observed on v1 or v2 endpoints — unchanged.
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic KKX3382745 is not a valid API secret — re-confirmed.
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A (Der bereitgestellte X-API-Secret ist ungültig oder nicht 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 erforderlich; X-A
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 19:37:36 UTC
- [70] kassenkompass.net: Whole-funnel attribution-cookie stuffing → partner commission/lead hijack (from art/lead_bigpickle.txt)
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request scoped test X-API-Secret + partner-portal account via bugs.olivermaicher.eu to close the two highest-value hypotheses — funnel attribution-cookie
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target); sets identical unvalidated pass-param att
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie in one response when both `jid` and `customerid` passed (jid alias then direct; last-wins a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params are NOT reflected into HTML (0 hits for probe tokens in 200 body) — cookie mirror only, no stored/reflected XSS v
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set a cookie on bonusrechner this probe — single-sample; alias map may be entry-specific (termin vs 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A (Der bereitgestellte X-API-Secret ist ungültig oder nicht 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 erforderlich; X-A
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 21:47:42 UTC
- [70] kassenkompass.de: Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year (from art/lead_nemotron3.txt)
- [55] api.kassenkompass.de: Undocumented v2 route beyond v1-mirror set — enumeration gap on router-404 oracle (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.kassenkompass.de/v2/health/ (compare body to recorded router-404 baseline; sweep continues at 1 rps: /v2/admin/, /v2/internal/, /v2/swagg
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 sweep gap confirmed — prior 24-name sweep omitted non-v1-mirror names (health/admin/internal/docs/schema/swagger/opena
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: X-API-Secret via query-string/cookie never tested — prior "sole channel" proof covers header names + api_key query only; 
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Set-Cookie write primitive (setcookie vs header) undetermined; CRLF discriminator probe chosen on .net to avoid Cloudflare v
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target); sets identical unvalidated pass-param att
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie in one response when both `jid` and `customerid` passed (jid alias then direct; last-wins a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params are NOT reflected into HTML (0 hits for probe tokens in 200 body) — cookie mirror only, no stored/reflected XSS v
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set a cookie on bonusrechner this probe — single-sample; alias map may be entry-specific (termin vs 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the prote
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400

## RANKED HYPOTHESES 2026-09-05 23:48:57 UTC
- [70] kassenkompass.de: Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year (from art/lead_nemotron3.txt)
- [68] kassenkompass.de: Attribute-cookie stuffing persists raw pass-params into 1-yr identification cookies; downstream commission/settlement consumption unproven without partner session (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Request scoped test X-API-Secret (A+B stacks) + partner-portal broker account via bugs.olivermaicher.eu — passive surface exhausted: v2 enumeration satur
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} belongs to middleware B ("X-API-Secret Header fehlt", instance-first) with /user/{ext_id}; six data GETs
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on middleware A, B, and v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded on write (%0D%0A literal) or suppressed for raw CRLF
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated — 42 names incl. infra (health/admin/internal/docs/swagger/schema/beta/staging/version/draft
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from active alias map; lizzen→afilcode is bonu
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params and cookies are host-only (.net≠.de registrable) — .net-attributed cookies unreadable by .d
- LEARN: ACCEPTED MISCONFIG @ api: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete.
- LEARN: REJECTED AUTH @ api: query-string AND cookie X-API-Secret both missing-header 401 on A/B/v2 — header sole channel.
- LEARN: REJECTED OTHER @ net: CRLF injection impossible — URL-encoded or suppressed cookie values.
- LEARN: REJECTED MISCONFIG @ api: v2 enumeration saturated at single endpoint (42 names).
- LEARN: ACCEPTED OTHER @ de: frab unmapped on both entries (2 sessions); lizzen→afilcode bonusrechner-specific.
- LEARN: ACCEPTED OTHER @ net: 302 no-param + host-only cookies ⇒ .net attribution not readable by .de.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target); sets identical unvalidated pass-param att
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie in one response when both `jid` and `customerid` passed (jid alias then direct; last-wins a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params are NOT reflected into HTML (0 hits for probe tokens in 200 body) — cookie mirror only, no stored/reflected XSS v
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set a cookie on bonusrechner this probe — single-sample; alias map may be entry-specific (termin vs 

## RANKED HYPOTHESES 2026-09-06 04:12:41 UTC
- [62] api.kassenkompass.de: Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://ka
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target); sets identical unvalidated pass-param att
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie in one response when both `jid` and `customerid` passed (jid alias then direct; last-wins a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params are NOT reflected into HTML (0 hits for probe tokens in 200 body) — cookie mirror only, no stored/reflected XSS v
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set a cookie on bonusrechner this probe — single-sample; alias map may be entry-specific (termin vs 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated — 42 names incl. infra (health/admin/internal/docs/swagger/schema/beta/staging/version/draft
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on middleware A, B, and v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded on write (%0D%0A literal) or suppressed for raw CRLF
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from active alias map; lizzen→afilcode is bonu
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params and cookies are host-only (.net≠.de registrable) — .net-attributed cookies unreadable by .d

## RANKED HYPOTHESES 2026-09-06 08:51:55 UTC
- [85] kassenkompass.de/bonusrechner.php: Funnel Parameter-to-Cookie Injection — Unvalidated Identity Fields Persisted for 1 Year (from art/lead_nemotron3.txt)
- [70] kassenkompass.de: Funnel attribution-cookie stuffing at multiple steps → lead/settlement poison (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_vergleich2.php?lizzen=KKL99&jid=KKJ99&agn=KKA9&ppn=KKP9&connectionnumber=KKC99&employeenumber=KKE99 (1 rps, cap
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.net/bonusrechner.php?frab=fr33 — test frab cookie setting on .net (passive, HEAD/GET, 1 rps); GET https://kassenkompass.net/bon
- LEARN: ACCEPTED MISCONFIG @ de: bonusrechner_daten.php is a second cookie-mirror entry (jid/agn/ppn→1yr HttpOnly) but ignores lizzen (no afilcode) — step-scoped alias 
- LEARN: ACCEPTED OTHER @ awv: client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400-on-invalid live;
- LEARN: REJECTED MISCONFIG @ net: all *.php → 302 bare-domain root, no per-name differential; param-less GET sets no attribution cookies.
- LEARN: REJECTED XSS @ api: v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no injection primitive.
- LEARN: ACCEPTED OTHER @ de: AWS S3 asset kk-s3-01 (public reads, list denied) + HubSpot 146866466 — new cloud/third-party surface, no exposure.
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: Funnel parameter-to-cookie injection confirmed live — raw params mirrored into 1-year cookies with no val
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 stack confirmed;
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated at 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-06 12:51:34 UTC
- [85] kassenkompass.de/bonusrechner.php: Funnel Parameter-to-Cookie Injection — Unvalidated Identity Fields Persisted for 1 Year (from art/lead_nemotron3.txt)
- [70] kassenkompass.de: Funnel multi-step cookie-stuffing → lead/settlement poison (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_vergleich2.php?lizzen=KKL99&jid=KKJ99&agn=KKA9&ppn=KKP9&connectionnumber=KKC99&employeenumber=KKE99 — 1 rps, ca
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.net/bonusrechner.php?frab=fr33 — test frab cookie setting on .net (passive, HEAD/GET, 1 rps)
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-AP
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code mi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning d
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the pr
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path ident
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDom
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenk
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend (og:url, canonical link, form POST target); sets identical unvalidated pass-param att
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie in one response when both `jid` and `customerid` passed (jid alias then direct; last-wins a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params are NOT reflected into HTML (0 hits for probe tokens in 200 body) — cookie mirror only, no stored/reflected XSS v
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set a cookie on bonusrechner this probe — single-sample; alias map may be entry-specific (termin vs 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated — 42 names incl. infra (health/admin/internal/docs/swagger/schema/beta/staging/version/draft
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on middleware A, B, and v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded on write (%0D%0A literal) or suppressed for raw CRLF
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from active alias map; lizzen→afilcode is bonu
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params and cookies are host-only (.net≠.de registrable) — .net-attributed cookies unreadable by .d
- LEARN: ACCEPTED MISCONFIG @ de: bonusrechner_daten.php is a second cookie-mirror entry (jid/agn/ppn→1yr HttpOnly) but ignores lizzen (no afilcode) — step-scoped alias 
- LEARN: ACCEPTED OTHER @ awv: client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400-on-invalid live;
- LEARN: REJECTED MISCONFIG @ net: all *.php → 302 bare-domain root, no per-name differential; param-less GET sets no attribution cookies
- LEARN: REJECTED XSS @ api: v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no injection primitive
- LEARN: ACCEPTED OTHER @ de: AWS S3 asset kk-s3-01 (public reads, list denied) + HubSpot 146866466 — new cloud/third-party surface, no exposure
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: Funnel parameter-to-cookie injection confirmed live — raw params mirrored into 1-year cookies with no val
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 stack confirmed;
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated at 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-06 16:14:12 UTC
- [75] kassenkompass.de/bonusrechner_fragen.php: Multi-Step Funnel Cookie Stuffing — Downstream Steps Consume Injected Identities (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_daten.php?jid=VICTIM123&agn=ADV456&ppn=PART789 — capture Set-Cookie headers for HttpOnly customerid/agenturnumm
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent, no misconfiguration
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categ
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` all reach protected handler (401); kk_id not validated a
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URLs/webhook/fetch in catalog; no metadata path
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` not a valid API secret
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex identical security headers; AWS ALB backend confirmed
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel mirrors raw pass-params into 1-year cookies with no validation — alias map jid|customerid→customerid, agn|connectionnu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (SGTM proxy) + load.awv.kassenkompass.de (Cloudflare-challenged) — JS-discovered
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info only registered v2 route (42 names → router-404); single-endpoint surface
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A; only /user/{ext_id} middleware B; /sync/ legacy HTTP-200;
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X-API-Secr
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface; root returns 404
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend; sets identical unvalidated attribution cookies then 302→.de; new inventory host
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie when both `jid` and `customerid` passed (jid alias then direct; last-wins ambiguity)
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params NOT reflected into HTML (0 hits for probe tokens) — cookie mirror only, no XSS via these params
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set cookie on bonusrechner — dropped from active alias map; lizzen→afilcode is bonusrechner-specific
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated at 42 names — insurance_info sole route
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on A/B/v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded or suppressed
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from alias map
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params + host-only cookies ⇒ .net cookies unreadable by .de
- LEARN: ACCEPTED MISCONFIG @ de: bonusrechner_daten.php second cookie-mirror entry (jid/agn/ppn→1yr HttpOnly) but ignores lizzen — step-scoped alias map, stuffing surfa
- LEARN: ACCEPTED OTHER @ awv: client container fully read — SGTM(Stape)/GA4/FB/purchase(128 EUR); /g/collect 400-on-invalid; "GTM proxy" label superseded by SGTM
- LEARN: REJECTED MISCONFIG @ net: all *.php → 302 bare-domain root, no per-name differential; param-less GET sets no attribution cookies
- LEARN: REJECTED XSS @ api: v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no injection primitive
- LEARN: ACCEPTED OTHER @ de: AWS S3 asset kk-s3-01 (public reads, list denied) + HubSpot 146866466 — new cloud/third-party surface, no exposure
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: Funnel parameter-to-cookie injection confirmed live — raw params mirrored into 1-year cookies with no val
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 confirmed; cooki
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-06 18:32:22 UTC
- [75] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel multi-step cookie-stuffing → lead/settlement attribution poison (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner.php (no params) vs with cookies `customerid=KKJ99; agenturnummer=KKC99; poolpartnernummer=KKP9; employeenumber=
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_daten.php?jid=VICTIM123&agn=ADV456&ppn=PART789 — capture Set-Cookie headers for HttpOnly customerid/agenturnumm
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_vergleich2.php tercer mirror entry — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; lizzen ignored (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de: termin.php + bonusrechner_suche.php are 4th/5th mirror entries (jid/agn/connectionnumber/employeenumber); stuffing surface ≥5
- LEARN: ACCEPTED OTHER @ kassenkompass.de: connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins) — same ambiguity class as jid/customerid 
- LEARN: REJECTED XSS @ kassenkompass.de: 0 HTML reflections of KKJ99/KKA9/KKC99/KKP9/KKE99/KKL99 on vergleich2 + termin — pure cookie mirror, no stored/reflected XSS.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent, no misconfiguration
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categ
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` all reach protected handler (401); kk_id not validated a
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URLs/webhook/fetch in catalog; no metadata path
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` not a valid API secret
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex identical security headers; AWS ALB backend confirmed
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel mirrors raw pass-params into 1-year cookies with no validation — alias map jid|customerid→customerid, agn|connectionnu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (SGTM proxy) + load.awv.kassenkompass.de (Cloudflare-challenged) — JS-discovered
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info only registered v2 route (42 names → router-404); single-endpoint surface
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A; only /user/{ext_id} middleware B; /sync/ legacy HTTP-200;
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X-API-Secr
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface; root returns 404
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend; sets identical unvalidated attribution cookies then 302→.de; new inventory host
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie when both `jid` and `customerid` passed (jid alias then direct; last-wins ambiguity)
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params NOT reflected into HTML (0 hits for probe tokens) — cookie mirror only, no XSS via these params
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set cookie on bonusrechner — dropped from active alias map; lizzen→afilcode is bonusrechner-specific
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated at 42 names — insurance_info sole route
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on A/B/v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded or suppressed
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from alias map
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params + host-only cookies ⇒ .net cookies unreadable by .de
- LEARN: ACCEPTED MISCONFIG @ de: bonusrechner_daten.php second cookie-mirror entry (jid/agn/ppn→1yr HttpOnly) but ignores lizzen — step-scoped alias map, stuffing surfa
- LEARN: ACCEPTED OTHER @ awv: client container fully read — SGTM(Stape)/GA4/FB/purchase(128 EUR); /g/collect 400-on-invalid; "GTM proxy" label superseded by SGTM
- LEARN: REJECTED MISCONFIG @ net: all *.php → 302 bare-domain root, no per-name differential; param-less GET sets no attribution cookies
- LEARN: REJECTED XSS @ api: v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no injection primitive
- LEARN: ACCEPTED OTHER @ de: AWS S3 asset kk-s3-01 (public reads, list denied) + HubSpot 146866466 — new cloud/third-party surface, no exposure
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: Funnel parameter-to-cookie injection confirmed live — raw params mirrored into 1-year cookies with no val
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 confirmed; cooki
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-06 20:53:42 UTC
- [75] kassenkompass.de/bonusrechner_daten.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [56] kassenkompass.de: Funnel attribution-cookie stuffing → server-side lead/settlement rewrite at POST/lead-write, GET-path unobservable (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_daten.php?jid=VICTIM123&agn=ADV456&ppn=PART789 — capture Set-Cookie headers for HttpOnly customerid/agenturnumm
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated s
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent, no misconfiguration
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categ
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catc
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` all reach protected handler (401); kk_id not validated a
- LEARN: REJECTED SSRF @ api.kassenkompass.de: No user-supplied URLs/webhook/fetch in catalog; no metadata path
- LEARN: REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT
- LEARN: REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` not a valid API secret
- LEARN: REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex identical security headers; AWS ALB backend confirmed
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Funnel mirrors raw pass-params into 1-year cookies with no validation — alias map jid|customerid→customerid, agn|connectionnu
- LEARN: ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (SGTM proxy) + load.awv.kassenkompass.de (Cloudflare-challenged) — JS-discovered
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info only registered v2 route (42 names → router-404); single-endpoint surface
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A; only /user/{ext_id} middleware B; /sync/ legacy HTTP-200;
- LEARN: REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X-API-Secr
- LEARN: REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths — closed completely
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface; root returns 404
- LEARN: ACCEPTED OTHER @ kassenkompass.net: Canonical IIS/10.0 + PHP 8.4.3 backend; sets identical unvalidated attribution cookies then 302→.de; new inventory host
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Attribution cookie attributes asymmetric — `afilcode` lacking Secure/HttpOnly; `customerid`/`agenturnummer`/`poolpartnernumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Duplicate `customerid` Set-Cookie when both `jid` and `customerid` passed (jid alias then direct; last-wins ambiguity)
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Pass-params NOT reflected into HTML (0 hits for probe tokens) — cookie mirror only, no XSS via these params
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: `frab` param did NOT set cookie on bonusrechner — dropped from active alias map; lizzen→afilcode is bonusrechner-specific
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 enumeration saturated at 42 names — insurance_info sole route
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both missing-header 401 on A/B/v2 — header strictly sole channel
- LEARN: REJECTED OTHER @ kassenkompass.net: CRLF header/cookie injection impossible — Set-Cookie values URL-encoded or suppressed
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; 15/15 map complete
- LEARN: ACCEPTED OTHER @ kassenkompass.de: frab sets NO cookie on termin.php OR bonusrechner.php (two sessions) — dropped from alias map
- LEARN: ACCEPTED OTHER @ kassenkompass.net: funnel 302→.de carries no params + host-only cookies ⇒ .net cookies unreadable by .de
- LEARN: ACCEPTED MISCONFIG @ de: bonusrechner_daten.php second cookie-mirror entry (jid/agn/ppn→1yr HttpOnly) but ignores lizzen — step-scoped alias map, stuffing surfa
- LEARN: ACCEPTED OTHER @ awv: client container fully read — SGTM(Stape)/GA4/FB/purchase(128 EUR); /g/collect 400-on-invalid; "GTM proxy" label superseded by SGTM
- LEARN: REJECTED MISCONFIG @ net: all *.php → 302 bare-domain root, no per-name differential; param-less GET sets no attribution cookies
- LEARN: REJECTED XSS @ api: v2 404 oracle decodes+mirrors path but JSON content-type + escaped — no injection primitive
- LEARN: ACCEPTED OTHER @ de: AWS S3 asset kk-s3-01 (public reads, list denied) + HubSpot 146866466 — new cloud/third-party surface, no exposure
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: Funnel parameter-to-cookie injection confirmed live — raw params mirrored into 1-year cookies with no val
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 confirmed; cooki
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-06 22:53:40 UTC
- [80] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel attribution-cookie stuffing → server-side consumption at POST submit / partner-portal settlement ingest only (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: In partner portal (KassenKompass partner login), search settlement/lead records for stuffed tokens KKJ99/KKA9/KKC99/KKP9/KKE99 set via kassenkompass.de/b
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — capture Set-Cookie headers and response size (known 2.1MB inline tariff data per KB; passive, 1 rp
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes in
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: settlement_report CSV/JSON format variants (catalog: "Cassatis Prime CSV-Download bzw. /json") probed — /json /csv ?forma
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: /health/ unchanged single unprotected endpoint (200 {status:ok}, cloudflare fronting confirmed on api this env, PHP 8
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_daten.php: Second funnel mirror entry confirmed — jid/agn/ppn→1yr HttpOnly cookies; ignores lizenz/no afilcode
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_vergleich2.php: Third mirror entry confirmed — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; conne
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/termin.php: Fourth mirror entry confirmed — jid/agn/connectionnumber/employeenumber→1yr HttpOnly; connectionnumber→agenturn
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_suche.php: Fifth mirror entry confirmed — same alias map as termin.php
- LEARN: ACCEPTED OTHER @ kassenkompass.net/bonusrechner.php: Canonical IIS/10.0 backend mirrors identical cookie injection then 302→.de; cookies host-only on .net
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: Greedy segment match confirmed — /v2/insurance_info/{anything} all reach auth handler (401); kk_id
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte, parameter pollution (last-wins), trailing space handled identically on .de and .net;
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner.php: afilcode param is `lizenz` (not `lizzen`); sets without Secure/HttpOnly; other cookies HttpOnly
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}

## RANKED HYPOTHESES 2026-09-07 00:53:46 UTC
- [80] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: Middleware-B IDOR — /user/{ext_id} and /cancel/{id} cross-tenant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Obtain a scoped partner/kk_webapp scope X-API-Secret test credential — then run sequential GET /user/{n} diff sweep (middleware B IDOR, target api); pass
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — capture Set-Cookie headers, response size, and body differential vs base (known 2.1MB inline tarif
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Root (/ , 15 v1, ver 1.0) + /v2/ (sole insurance_info, ver 2.0) catalogs stable — no endpoint drift; re-confirmed live.
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: access-control-allow-headers/allow-methods identical on middleware A and B; no origin reflection — implies JS-delivered s
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Middleware-B greedy match confirmed — /user/ empty segment routes to B (401 "fehlt"); "instance echo" = RFC 9457 path, no
- LEARN: REJECTED OTHER @ kassenkompass.de: bonusrechner2/alt/detail/informiert/berechnung/ergebnis/upload all 404 on .de — stuffing surface capped at 5 confirmed mirror
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_daten.php: Second funnel mirror entry confirmed — jid/agn/ppn→1yr HttpOnly cookies; ignores lizenz/no afilcode
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_vergleich2.php: Third mirror entry confirmed — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; conne
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/termin.php: Fourth mirror entry confirmed — jid/agn/connectionnumber/employeenumber→1yr HttpOnly; connectionnumber→agenturn
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_suche.php: Fifth mirror entry confirmed — same alias map as termin.php
- LEARN: ACCEPTED OTHER @ kassenkompass.net/bonusrechner.php: Canonical IIS/10.0 backend mirrors identical cookie injection then 302→.de; cookies host-only on .net
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: Greedy segment match confirmed — /v2/insurance_info/{anything} all reach auth handler (401); kk_id
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte, parameter pollution (last-wins), trailing space handled identically on .de and .net;
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner.php: afilcode param is `lizenz` (not `lizzen`); sets without Secure/HttpOnly; other cookies HttpOnly
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: settlement_report CSV/JSON format variants probed — /json /csv ?format=csv .json all middleware-A 401 RFC 9457 problem+js
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: /health/ unchanged single unprotected endpoint (200 {status:ok}, cloudflare fronting confirmed, PHP 8.4.3 x-powered-b
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 confirmed; cooki
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated at 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-07 05:58:14 UTC
- [80] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel cookie-stuffing → server-side lead/commission poisoning at partner portal ingest (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — capture Set-Cookie headers, response size, and body differential vs base (2.1MB inline tariff blob
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response size, body differential vs base, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner2/alt/detail/informiert/berechnung/ergebnis/upload all 404 — stuffing surface capped at 5 confirmed mirrors + fra
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: access-control-allow-headers/allow-methods identical on middleware A and B; no origin reflection — JS-delivered secret, c
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential byte-identical (standard.js?v= cache-buster + cfemail nonce drift o
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Root (/ , 15 v1, ver 1.0) + /v2/ (sole insurance_info, ver 2.0) catalogs stable — no endpoint drift; re-confirmed live.
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: access-control-allow-headers/allow-methods identical on middleware A and B; no origin reflection — implies JS-delivered s
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Middleware-B greedy match confirmed — /user/ empty segment routes to B (401 "fehlt"); "instance echo" = RFC 9457 path, no
- LEARN: REJECTED OTHER @ kassenkompass.de: bonusrechner2/alt/detail/informiert/berechnung/ergebnis/upload all 404 on .de — stuffing surface capped at 5 confirmed mirror
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_daten.php: Second funnel mirror entry confirmed — jid/agn/ppn→1yr HttpOnly cookies; ignores lizenz/no afilcode
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_vergleich2.php: Third mirror entry confirmed — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; conne
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/termin.php: Fourth mirror entry confirmed — jid/agn/connectionnumber/employeenumber→1yr HttpOnly; connectionnumber→agenturn
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_suche.php: Fifth mirror entry confirmed — same alias map as termin.php.
- LEARN: ACCEPTED OTHER @ kassenkompass.net/bonusrechner.php: Canonical IIS/10.0 backend mirrors identical cookie injection then 302→.de; cookies host-only on .net.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: Greedy segment match confirmed — /v2/insurance_info/{anything} all reach auth handler (401); kk_id
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route.
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte, parameter pollution (last-wins), trailing space handled identically on .de and .net;
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner.php: afilcode param is `lizenz` (not `lizzen`); sets without Secure/HttpOnly; other cookies HttpOnly.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}.
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: settlement_report CSV/JSON format variants probed — /json /csv ?format=csv .json all middleware-A 401 RFC 9457 problem+js
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: /health/ unchanged single unprotected endpoint (200 {status:ok}, Cloudflare fronting confirmed, PHP 8.4.3 x-powered-b
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.net/bonusrechner.php: Canonical backend mirrors identical cookie injection then 302→.de; IIS/10.0 + PHP 8.4.3 confirmed; cooki
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: v2 shares middleware A with v1 majority; greedy segment match confirmed; enumeration saturated at 
- LEARN: REJECTED AUTH @ api.kassenkompass.de: X-API-Secret via query-string AND cookie both return missing-header 401 on all stacks — header strictly sole channel.
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}.
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-07 12:16:46 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response size, body differential vs base, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php confirmed as 6th funnel step — 200 response, potential settlement submission endpoint
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data response confirmed — unauthenticated, no rate limit, competitive intelli

## RANKED HYPOTHESES 2026-09-07 18:00:41 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel cookie-stuffing → server-side lead/commission poisoning at partner portal ingest (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — capture Set-Cookie headers, response size (2.1MB known), and body differential vs base; test wheth
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://kassenkompass.de/bonusrechner_abschluss.php with minimal form data (email=test%40example.com, password=Test123%21, password_confirm=Test123%
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Root (/ , 15 v1, ver 1.0) + /v2/ (sole insurance_info, ver 2.0) catalogs stable — no endpoint drift; re-confirmed live.
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: access-control-allow-headers/allow-methods identical on middleware A and B; no origin reflection — implies JS-delivered s
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Middleware-B greedy match confirmed — /user/ empty segment routes to B (401 "fehlt"); "instance echo" = RFC 9457 path, no
- LEARN: REJECTED OTHER @ kassenkompass.de: bonusrechner2/alt/detail/informiert/berechnung/ergebnis/upload all 404 on .de — stuffing surface capped at 5 confirmed mirror
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_daten.php: Second funnel mirror entry confirmed — jid/agn/ppn→1yr HttpOnly cookies; ignores lizenz/no afilcode
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_vergleich2.php: Third mirror entry confirmed — jid/agn/connectionnumber/ppn/employeenumber→1yr HttpOnly; conne
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/termin.php: Fourth mirror entry confirmed — jid/agn/connectionnumber/employeenumber→1yr HttpOnly; connectionnumber→agenturn
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_suche.php: Fifth mirror entry confirmed — same alias map as termin.php.
- LEARN: ACCEPTED OTHER @ kassenkompass.net/bonusrechner.php: Canonical IIS/10.0 backend mirrors identical cookie injection then 302→.de; cookies host-only on .net.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2/insurance_info/: Greedy segment match confirmed — /v2/insurance_info/{anything} all reach auth handler (401); kk_id
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: Enumeration saturated at 42 names — insurance_info sole route.
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte, parameter pollution (last-wins), trailing space handled identically on .de and .net;
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner.php: afilcode param is `lizenz` (not `lizzen`); sets without Secure/HttpOnly; other cookies HttpOnly.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}.
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php confirmed as 6th funnel step — 200 response, POST form for account creation, full superset alias m
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins ambiguity) — sa
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data response confirmed — unauthenticated, no rate limit, competitive intelli

## RANKED HYPOTHESES 2026-09-07 21:29:13 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel cookie-stuffing → server-side lead/commission poisoning at partner-portal ingest, now self-verifiable via open registration (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: With human go-ahead, run the self-registration stuffing test — set stuffed mirror cookies (customerid=KKJ99, agenturnummer=KKG77+KKC99, poolpartnernummer
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://kassenkompass.de/bonusrechner_abschluss.php with minimal form data (email=test%40example.com, password=Test123%21, password_confirm=Test123%
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: blob internals — sessionData (akt_kk_id/available_kk_uids empty anon), ucatKkData (1.79MB per-KK reso
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: protected insurance_info payload domain is publicly replicated by fragen.php ucatKkData — BOLA cross-tenant read v
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: open self-registration (email/password/confirm, create_account=1, no CAPTCHA, self-submit POST) pr
- LEARN: REJECTED OTHER @ kassenkompass.de: no X-API-Secret/Bearer/api_key strings in public bonusrechner frontend — JS-delivered-secret inference unsupported on this su
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php confirmed as 7th funnel step — 200 response, POST form for account creation, full superset alias m
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins ambiguity) — sa
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data response confirmed — unauthenticated, no rate limit, competitive intelli

## RANKED HYPOTHESES 2026-09-07 23:48:01 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://kassenkompass.de/bonusrechner_abschluss.php with minimal form data (email=test%40example.com, password=Test123%21, password_confirm=Test123%
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php confirmed as 7th funnel step — 200 response, POST form for account creation, full superset alias m
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins ambiguity) — sa
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data response confirmed — unauthenticated, no rate limit, competitive intelli

## RANKED HYPOTHESES 2026-09-08 04:14:37 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] kassenkompass.de: Funnel cookie-stuffing → server-side lead/commission poisoning (step-scoped alias divergence included) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://kassenkompass.de/bonusrechner_abschluss.php with minimal form data (email=test%40example.com, password=Test123%21, password_confirm=Test123%
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php confirmed as 7th funnel step — 200 response, POST form for account creation, full superset alias m
- LEARN: ACCEPTED OTHER @ kassenkompass.de: bonusrechner_abschluss.php connectionnumber→agenturnummer dual alias produces duplicate Set-Cookie (last-wins ambiguity) — sa
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully read — SGTM(Stape ahcfuvbcz)/GA4 G-RXB3GJEMRT/FB 360390300088445/purchase(128 EUR); /g/collect 400
- LEARN: ACCEPTED OTHER @ kassenkompass.de: kk-s3-01 layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid); no other prefixes; i
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data response confirmed — unauthenticated, no rate limit, competitive intelli

## RANKED HYPOTHESES 2026-09-08 09:16:02 UTC
- [70] kassenkompass.de: Cookie-stuffing persistence through self-registration flow — stuffed attribution cookies consumed at account creation (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumber=KKE99 — capture all Set-Cookie headers; (2) POS

## RANKED HYPOTHESES 2026-09-08 13:49:29 UTC
- [70] kassenkompass.de: Cookie-stuffing persistence through self-registration flow — stuffed attribution cookies consumed at account creation (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumber=KKE99 — capture all Set-Cookie headers; (2) POS
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: open self-registration (email/password/confirm, create_account=1, no CAPTCHA, self-submit POST) pr
- LEARN: REJECTED OTHER @ kassenkompass.de: no X-API-Secret/Bearer/api_key strings in public bonusrechner frontend — JS-delivered-secret inference unsupported on this su

## RANKED HYPOTHESES 2026-09-08 17:45:17 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [70] kassenkompass.de/bonusrechner_abschluss.php: Cookie-stuffing persistence through self-registration flow — stuffed attribution cookies consumed at account creation (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumber=KKE99 — capture all Set-Cookie headers; (2) POS
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: open self-registration (email/password/confirm, create_account=1, no CAPTCHA, self-submit POST) pr
- LEARN: REJECTED OTHER @ kassenkompass.de: no X-API-Secret/Bearer/api_key strings in public bonusrechner frontend — JS-delivered-secret inference unsupported on this su
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m

## RANKED HYPOTHESES 2026-09-08 20:23:43 UTC
- [80] kassenkompass.de/bonusrechner_abschluss.php: Cookie-Stuffing Persistence Through Self-Registration Flow — Stuffed Attribution Cookies Consumed at Account Creation (from art/lead_nemotron3.txt)
- [78] kassenkompass.de/bonusrechner_abschluss.php: Step-scoped alias divergence enables cross-step attribution forging — stuffed cookies persist through self-registration settlement (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumber=KKE99 — capture token-value Set-Cookie set; (2)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Cookie-stuffing persistence chain has been machine-verifiable since 2026-09-08 13:49 via abschluss.php self-registration but 
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m

## RANKED HYPOTHESES 2026-09-08 22:50:10 UTC
- [80] kassenkompass.de/bonusrechner_abschluss.php: Cookie-Stuffing Persistence Through Self-Registration Flow — Stuffed Attribution Cookies Consumed at Account Creation (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de: Middleware-B IDOR — /user/{ext_id} and /cancel/{id} cross-tenant access under shared B-scoped secret (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumber=KKE99 — capture all Set-Cookie headers; (2) POS
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: open self-registration (email/password/confirm, create_account=1, no CAPTCHA, self-submit POST) pr
- LEARN: REJECTED OTHER @ kassenkompass.de: no X-API-Secret/Bearer/api_key strings in public bonusrechner frontend — JS-delivered-secret inference unsupported on this su
- LEARN: ACCEPTED OTHER @ kassenkompass.de: Cookie-stuffing persistence chain has been machine-verifiable since 2026-09-08 13:49 via abschluss.php self-registration but 
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 01:14:07 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (refined by Account-ID gate) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: chain the lead-init sequence under the stuffed jar — (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeen
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner.php: 7/7 funnel mirror re-confirmed live — lizenz→afilcode (no Secure/HttpOnly), jid→customerid, agn→agenturnumme
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 06:12:53 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (refined by Account-ID gate) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: chain the lead-init sequence under stuffed jar — (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumbe
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 11:43:00 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (refined by Account-ID gate) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: chain the lead-init sequence under stuffed jar — (1) GET https://kassenkompass.de/bonusrechner.php?lizenz=KKA9&jid=KKJ99&agn=KKG77&ppn=KKP9&employeenumbe
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 15:36:36 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [80] kassenkompass.de: Cookie-Stuffing Attribution Theft Via Unvalidated 1-Year Affilcode Persistence (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: consult knowledge base for any partner/settlement evidence that would close the AUTH_HELPED gap on cookie-stuffing attribution theft — specifically whether
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential discovered — "Account-ID nicht gefunden" present ONLY on POST, absent 
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "One-shot stuffing→register auto-creates account" REFUTED — full 4-step chain (entry→daten→fragen→
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: Root + v2 catalogs stable (15 v1 + 1 v2 endpoint, ver 1.0/2.0) — zero drift since 2026-09-07. API surface remains credent
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 18:47:54 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Confirmed 7th funnel step with open self-registration (email/password/confirm, create_account=1, n
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Accepts full superset alias map (lizenz→afilcode non-HttpOnly; jid→customerid; agn+connectionnumbe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (ucatKkData 1.79MB per-KK resolved refs, lastchange 2026-05-03, globalbu
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de/v2: Protected insurance_info payload domain (draft categories + resolved references) publicly replicated by bonusrechner_f
- LEARN: ACCEPTED OTHER @ awv.kassenkompass.de: Client container fully characterized — SGTM (Stape ahcfuvbcz), GA4 G-RXB3GJEMRT, FB 360390300088445, purchase event 128 E
- LEARN: ACCEPTED OTHER @ kk-s3-01.s3.eu-central-1.amazonaws.com: Layout fully mapped — 174 refs all uploads/fraq/{qid}/{n}.png question images (sequential qid), images-
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar
- LEARN: REJECTED OTHER @ kassenkompass.de: Subdomain sweep ~80 names (incl. kk-webapp/kk_webapp/partner/bonus) → only api/www/awv + load.awv exist; kk_webapp delegation
- LEARN: REJECTED OTHER @ kassenkompass.net: Parser differential tested — null byte (%00), parameter pollution (last-wins), trailing space handled identically on .de and
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-09 21:39:23 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [72] api.kassenkompass.de: Middleware-B IDOR — cross-tenant user read + destructive cancel/delete under one B-scoped secret (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/login_partner.php (200) → extract form action + <script src> list; then GET the partner-portal JS entry and grep for `X-API-
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-09 23:35:38 UTC
- [45] kassenkompass.de/login_partner.php: Partner-Portal Client Delivers B-Scoped X-API-Secret (unlocks B-stack IDOR) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/login_partner.php (200) and persist full body; extract `<form action>/method/fields` and `<script src>` list; then GET the p

## RANKED HYPOTHESES 2026-09-10 01:32:22 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- [45] kassenkompass.de/login_partner.php: Partner-Portal Client Delivers B-Scoped X-API-Secret (unlocks B-stack IDOR) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/login_partner.php → extract full HTML body (form action/method/fields + all `<script src>` URLs); then GET each JS asset → g
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_abschluss.php — capture Set-Cookie headers, response body, form action/method/fields, and any settlement/submis
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-10 06:44:21 UTC
- [85] kassenkompass.de/bonusrechner.php: Multi-Step Funnel Authorization Bypass Via Step-Scoped Alias Map Divergence (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/login_partner.php — extract full HTML body (form action/method/fields + all <script src> URLs); then GET each JS asset → gre
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-10 11:58:17 UTC
- [80] kassenkompass.de/bonusrechner_fragen.php: Large Inline Tariff Data Exposure — Unauthenticated 2.1MB Competitive Intelligence Leak (from art/lead_bigpickle.txt)
- [75] kassenkompass.de/bonusrechner_abschluss.php: Funnel Cookie Stuffing → Account Creation Via Lead-Gated POST Bypass (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: curl -sI https://kassenkompass.de/bonusrechner_fragen.php → extract Cache-Control, ETag, Last-Modified, Content-Length headers; then GET body once → conf
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/login_partner.php — extract full HTML body (form action/method/fields + all <script src> URLs); then GET each JS asset → gre
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-10 16:15:52 UTC
- [80] kassenkompass.de/bonusrechner_fragen.php: Large Inline Tariff Data Exposure — Unauthenticated 2.1MB Competitive Intelligence Leak (from art/lead_bigpickle.txt)
- [75] kassenkompass.de/bonusrechner_abschluss.php: Funnel Cookie Stuffing → Account Creation Via Lead-Gated POST Bypass (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: curl -sI https://kassenkompass.de/bonusrechner_fragen.php → extract Cache-Control, ETag, Last-Modified, Content-Length headers; then GET body once → conf
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/login_partner.php — extract full HTML body (form action/method/fields + all <script src> URLs); then GET each JS asset → gre
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: "Self-registration = automated verification surface for cookie-stuffing→account-creation" REFUTED 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-10 19:18:27 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated 2.1MB Tariff Database Served Per-Request With No Cache, No Rate Limit (VERIFIED) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HEAD https://kassenkompass.de/bonusrechner_abschluss.php?lizenz=BBPROBE&jid=BBJID&agn=BBAGN&ppn=BBPPN — confirm superset alias map under `lizenz` spellin
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: Registration server-side lead-gated — valid POST → 200 + unique "Account-ID nicht gefunden" div; b
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_fragen.php: 7/7 funnel mirror confirmed — lizenz→afilcode (non-Secure/HttpOnly), jid→customerid, agn+connectio
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: sessionData all null under stuffed jar — server does NOT read stuffed cookies for data population; ta
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED OTHER @ kassenkompass.de: GET branch closed 7/7 — base-vs-stuffed body differential on fragen/suche/vergleich2/abschluss/termin byte-identical (standar

## RANKED HYPOTHESES 2026-09-10 21:45:49 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [80] kassenkompass.de/bonusrechner_fragen.php: Cookie-Stuffing Attribution Theft Via Unvalidated 1-Year Affilcode Persistence (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: curl -sI https://kassenkompass.de/bonusrechner_fragen.php → extract Cache-Control, ETag, Last-Modified, Content-Length headers; then GET body once → conf
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-10 23:56:56 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HEAD https://kassenkompass.de/bonusrechner_abschluss.php?lizenz=BBPROBE&jid=BBJID&agn=BBAGN&ppn=BBPPN — confirm superset alias map under `lizenz` spellin
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 04:25:26 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [80] kassenkompass.de: Cookie-Stuffing Attribution Theft Via Unvalidated 1-Year Attribution Cookies (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: after WAF cooldown (≥60s), single HEAD https://kassenkompass.de/bonusrechner_fragen.php — confirm 200/2,158,150B persists post-block and no cache headers
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: payload internals parsed — ucatKkData 5,209 rows {uid_cat,uid_ucat_q,uid_kk_q,wert,wertart} 1.79M
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /api/ => IIS dir-listing-denied 403 (1233B) vs /uploads/,/fraq/,/images/ => 404 — physical /api/ dir exists at origin web roo
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /trace.axd => ASP.NET "Trace Error" + x-aspnet-version 4.0.30319 — IIS/ASP.NET 4.0 confirmed on .de origin (PHP coexists); re
- LEARN: ACCEPTED OTHER @ kassenkompass.de: www mirror serves identical 2.1MB fragen payload + identical lizenz/jid/agn/ppn 4-cookie injection on abschluss.php — stuffin
- LEARN: ACCEPTED OTHER @ kassenkompass.de: ~14-request burst triggered transient WAF IP-block ("Ihre IP wurde voruebergehend gesperrt", 149B 403 on benign+blocked paths
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 09:20:20 UTC
- [70] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 13:40:20 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: single GET https://kassenkompass.de/bonusrechner_fragen.php with verbose output (time, content-length, cache headers) — confirm 200/~2.1MB persists post-
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 17:16:53 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: after WAF cooldown (≥60s), single HEAD https://kassenkompass.de/bonusrechner_fragen.php — confirm 200/2,158,150B persists post-block and no cache headers
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: payload internals parsed — ucatKkData 5,209 rows {uid_cat,uid_ucat_q,uid_kk_q,wert,wertart} 1.79M
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /api/ => IIS dir-listing-denied 403 (1233B) vs /uploads/,/fraq/,/images/ => 404 — physical /api/ dir exists at origin web roo
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /trace.axd => ASP.NET "Trace Error" + x-aspnet-version 4.0.30319 — IIS/ASP.NET 4.0 confirmed on .de origin (PHP coexists); re
- LEARN: ACCEPTED OTHER @ kassenkompass.de: www mirror serves identical 2.1MB fragen payload + identical lizenz/jid/agn/ppn 4-cookie injection on abschluss.php — stuffin
- LEARN: ACCEPTED OTHER @ kassenkompass.de: ~14-request burst triggered transient WAF IP-block ("Ihre IP wurde voruebergehend gesperrt", 149B 403 on benign+blocked paths
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 19:54:26 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: after WAF cooldown (≥60s), single HEAD https://kassenkompass.de/bonusrechner_fragen.php — confirm 200/2,158,150B persists post-block and no cache headers
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: payload internals parsed — ucatKkData 5,209 rows {uid_cat,uid_ucat_q,uid_kk_q,wert,wertart} 1.79M
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /api/ => IIS dir-listing-denied 403 (1233B) vs /uploads/,/fraq/,/images/ => 404 — physical /api/ dir exists at origin web roo
- LEARN: ACCEPTED OTHER @ kassenkompass.de: /trace.axd => ASP.NET "Trace Error" + x-aspnet-version 4.0.30319 — IIS/ASP.NET 4.0 confirmed on .de origin (PHP coexists); re
- LEARN: ACCEPTED OTHER @ kassenkompass.de: www mirror serves identical 2.1MB fragen payload + identical lizenz/jid/agn/ppn 4-cookie injection on abschluss.php — stuffin
- LEARN: ACCEPTED OTHER @ kassenkompass.de: ~14-request burst triggered transient WAF IP-block ("Ihre IP wurde voruebergehend gesperrt", 149B 403 on benign+blocked paths
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-11 22:29:04 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [80] kassenkompass.de: Cookie-Stuffing Attribution Theft Via Unvalidated 1-Year Attribution Cookies (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 00:41:50 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: single GET https://api.kassenkompass.de/v2/ — verify versioned catalog (ver 2.0, insurance_info sole) integrated at the 2026-09-07 baseline; then STOP (W
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data served unauthenticated, no rate limit, sessionData null under stuffed ja
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED OTHER @ kassenkompass.de/bonusrechner_abschluss.php: One-shot stuffing→register auto-creates account REFUTED — full 4-step chain (entry→daten→fragen→ab
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id random per fresh session, sticky after issuance (1yr Secure HttpOnly SameSite=Lax), sol
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: no-store+CF-DYNAMIC → full 2.1MB tariff body regenerated per anonymous request; no ETag/Last-Modi
- LEARN: REJECTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: kk_id query param not consumed (akt_kk_id=null, identical payload three ways) — no per-KK amplifi
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_daten.php: mapa correction — daten.php mirrors lizenz→afilcode (non-HttpOnly) + jid/agn/ppn; prior "ignores lizze
- LEARN: ACCEPTED OTHER @ kassenkompass.de: attribution cookies not echoed at GET render (same-jar param-less request re-issues none) — mirror-once, cookie-jar-carries m
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 05:10:26 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A

## RANKED HYPOTHESES 2026-09-12 09:29:44 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 13:15:39 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [80] kassenkompass.de: Cookie-Stuffing Attribution Theft Via Unvalidated 1-Year Attribution Cookies (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PARKED — all three standing hypotheses require either AUTH_HELPED (cookie-stuffing, B-Stack IDOR) or are PASSIVE-VERIFIED (tariff DB). API surface saturated, en
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 16:27:24 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 18:50:03 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated 2.1MB Tariff Database Served Per-Request, No Cache, No Rate Limit (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PARKED: resume when either (a) B-scoped X-API-Secret for api.kassenkompass.de becomes available (test IDOR/BOLA on /user/, /cancel/, /settlement_report/), or (b
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root catalog disclosure (15 v1 + 1 v2, ver 1.0/2.0) persists without auth across 12 sessions; content-length header n
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: Root content-length anomaly (0) was transient — header now matches body; no lasting structural regression.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ HTTP 200 + 67B auth-error body (legacy) and v2 401 middleware-A gate both live and unchanged — auth map stable
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 21:23:53 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [70] kassenkompass.de/bonusrechner_vergleich2.php: API Root Catalog Disclosure Enables Targeted Attack Planning (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root catalog disclosure (15 v1 + 1 v2) + /sync/ HTTP-200 legacy body + v2 middleware-A gate all live and unchanged as
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable across 8 sessions incl. 2026-09-12 18:50 — no ETag/Last-Modified/rate
- LEARN: REJECTED OTHER @ kassenkompass pipeline: triage 21:15 consumed empty lead payload — no new findings from any agent this cycle; all 5 lead files header-only or r
- LEARN: REJECTED MISCONFIG @ kassenkompass.de: 2026-09-11 transient WAF IP-block not reproduced; maintaining ≤1 rps discipline; no further burst probes planned.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-12 23:23:17 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de/user/{ext_id}: B-Stack IDOR on /user/{ext_id} + /cancel/{id} (kk_webapp-delegation middleware) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: resume conditions unchanged — (a) B-scoped X-API-Secret available → GET /user/1..N diff PII, test /settlement_report/ BOLA; (b) funnel settlement POST endp
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-13 01:29:26 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [62] api.kassenkompass.de/user/{ext_id}: B-Stack IDOR on /user/{ext_id} + /cancel/{id} (kk_webapp-delegation middleware) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: PARKED — no live probes this cycle; smoke batch 23:23 already confirmed stability and the gap is 2h within the standing 3-h cadence. Resume only on (a) B-s
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED OTHER @ kassenkompass pipeline: triage runs 21:15/23:05 (12th) + 01:07 (13th) again consumed empty lead payloads — none of the 5 peer leads contributed
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: 23:23 batch reconfirmed 15+1 v2 catalogs, /sync/ HTTP-200 legacy body, middleware-A/B gates — auth map drift-free thr
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-13 06:52:18 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-13 12:45:45 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: maintain 3-GET weekly smoke cadence; flag if >24h batch gap
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-13 16:59:38 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — 3-GET smoke cadence healthy (last batch 06:47, ~6h gap, flag only at >24h); no new probe justified; next smoke batch per cadence re-fires fragen.php
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de/: root CL:0-with-body is PERSISTENT (09-12 23:23, 09-13 06:52/12:45) — 09-12 20:04 "transient" classification prematur
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no

## RANKED HYPOTHESES 2026-09-13 19:04:49 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 06:47 (~10h gap, trigger next 3-GET smoke only at >24h i.e. after 06:47 09-14); append the abschluss POST-body differential (c
- NEXT(hypotheses-nemotron3.txt): RAG: hold — 3-GET smoke cadence healthy (last batch 06:47, ~10h gap, flag only at >24h); no new probe justified; next smoke batch per cadence re-fires fragen.ph
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 5+ consecutive triage cycles (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59) consumed empty lead payloads — all peer
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de/: root CL:0-with-body PERSISTENT through 06:52/12:45 — cosmetic header/body mismatch, 15+1 catalog disclosure substanc
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 16:59 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; no new enumeration primit
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no

## RANKED HYPOTHESES 2026-09-13 21:28:39 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 06:47 09-13 (~15h gap now); trigger next 3-GET smoke only at >24h (after 06:47 09-14): fragen.php (200/CL 2,158,150), bonusrec
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 8 consecutive triage cycles (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/now) consumed empty lead payloads —
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 19:04 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body persi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no

## RANKED HYPOTHESES 2026-09-13 23:38:19 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 06:47 09-13 (~16.7h gap); trigger next 3-GET smoke only at >24h (after 06:47 09-14): fragen.php (200/CL 2,158,150), bonusrechn
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 8th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25) consumed empty/header-only 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 19:04 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body persi

## RANKED HYPOTHESES 2026-09-14 01:46:29 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 8th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25) consumed empty/header-only 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 19:04 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body persi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no

## RANKED HYPOTHESES 2026-09-14 07:13:37 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 01:46 09-14 (~5.4h ago); 24h smoke threshold (post-06:47 09-14) met but 01:46 batch already confirmed no drift; defer next 3-G
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 01:46 09-14 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable ≥10 sessions since 2026-09-07 — no ETag/Last-Modified/rate-limit regr
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: second consecutive analysis-only cycle since 06:47 batch; parity with 12:45 aggregation, no peer/self leads matured, no

## RANKED HYPOTHESES 2026-09-14 14:37:04 UTC
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 01:46 09-14 (~5.4h ago); 24h smoke threshold (post-06:47 09-14) met but 01:46 batch already confirmed no drift; defer next 3-G
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 01:46 09-14 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable ≥10 sessions since 2026-09-07 — no ETag/Last-Modified/rate-limit regr

## RANKED HYPOTHESES 2026-09-14 19:40:15 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 01:46 09-14 (~12.9h ago); 24h smoke threshold not met (due after 01:46 09-15). Next 3-GET smoke: fragen.php (200/CL 2,158,150)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural change from prior full-body catalo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty

## RANKED HYPOTHESES 2026-09-14 22:49:01 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — last live probe batch 01:46 09-14 (~12.9h ago); 24h smoke threshold not met (due after 01:46 09-15). Next 3-GET smoke: fragen.php (200/CL 2,158,150)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: live GET 22:47 measured 2,152,258 B vs recorded 2,158,150 — tariff payload drifts on data refresh
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: per-KK lastchange epochs are 2025 (1746314584=2025-05-03, max 1766419026=2025-12-22); prior "2026-05-
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty

## RANKED HYPOTHESES 2026-09-15 01:21:14 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 9th consecutive triage cycle (09-12 21:15/23:05, 09-13 01:07/06:47/12:45/16:59/19:04/21:25, 09-14 01:46) consumed empty
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: live GET 22:47 measured 2,152,258 B vs recorded 2,158,150 — tariff payload drifts on data refresh
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_fragen.php: per-KK lastchange epochs are 2025 (1746314584=2025-05-03, max 1766419026=2025-12-22); prior "2026-05-
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-15 06:23:20 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — 24h fragen.php smoke threshold not yet met (last measured 22:47 09-14; due after 22:47 09-15). No live probes warranted until then. All peer lead fi
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 01:46 09-14 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A; root CL:0-with-body
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload stable ≥10 sessions since 2026-09-07 — no ETag/Last-Modified/rate-limit regr
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th+ consecutive triage cycle consumed empty lead payloads — all peers repetition; observability gap persists, no sign
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-15 11:58:25 UTC
- [88] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: hold — 24h fragen.php smoke threshold not yet met (last measured 22:47 09-14; due after 22:47 09-15). No live probes warranted until then. All peer lead fi
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 06:18 09-15; 15+1 disclosure substance unchanged; no drift.
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB tariff payload confirmed at 06:18 09-15; 2,152,258 B matches 22:47 09-14; drift ±0.3% live-
- LEARN: ACCEPTED OTHER @ www.kassenkompass.de/bonusrechner_fragen.php: identical 2,152,258 B — tariff leak surface confirmed doubled apex+www.
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie + catoint force-delete — confirmed live at 06:18; sole funnel step emitting devi
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential re-confirmed — lead gate present only on POST.
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query/cookie X-API-Secret missing-header on A/B/v2 — header sole channel; closed 14+ sessions.
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: no new enumeration primitive — v2 saturated 42 names, auth source-merge closed, 15/15 map stable.
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th+ consecutive empty triage cycle — observability gap persists.
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-15 16:49:34 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [70] api.kassenkompass.de/: API Root Catalog Disclosure Enables Targeted Attack Planning (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- NEXT(hypotheses-nemotron3.txt): RAG: Query threat intel / peer leads for KassenKompass GmbH — 10th consecutive empty triage cycle, observability gap persists; check for new CVE disclosures, Gi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-15 20:08:44 UTC
- [88] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): RAG: HOLD until ≥22:47 09-15 (fragen.php 24h-smoke threshold; last measurement 22:47 09-14). At threshold, exactly 3 spaced 1-rps GETs: /bonusrechner_fragen.php
- NEXT(hypotheses-nemotron3.txt): RAG: Query threat intel / peer leads for KassenKompass GmbH — 10th consecutive empty triage cycle, observability gap persists; check for new CVE disclosures, Gi
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 11th consecutive triage cycle (16:49 09-15) — peer leads remain header-only/stub repetition; observability gap persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 16:49 09-15; 15+1 disclosure substance unchanged; auth map drift-free; no new primiti
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Root returns 200 with content-length: 0 but full JSON catalog in body — structural header/body mismatch persists; cat
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-15 23:00:42 UTC
- [88] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥22:47 09-15 (24h since 22:47 09-14 measurement), single 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh empty jar → expect HTTP
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 11th consecutive triage cycle (16:49 09-15) — peer leads remain header-only/stub repetition; observability gap persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 16:49 09-15; 15+1 disclosure substance unchanged; auth map drift-free; no new primiti
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-16 01:21:00 UTC
- [88] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: hold until ≥01:19 09-17 (24h since fragen.php 2,152,680 B measurement at 01:19 09-16). At threshold, single 1-rps GET https://kassenkompass.de/bonusrechn
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 01:19 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 12th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 11th consecutive triage cycle (16:49 09-15) — peer leads remain header-only/stub repetition; observability gap persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 16:49 09-15; 15+1 disclosure substance unchanged; auth map drift-free; no new primiti
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-16 06:21:00 UTC
- [85] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [80] kassenkompass.de: API Root Catalog Disclosure Enables Targeted Attack Planning (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: hold until ≥01:19 09-17 (24h since fragen.php 2,152,680 B measurement at 01:19 09-16). At threshold, single 1-rps GET https://kassenkompass.de/bonusrechn
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 11th consecutive triage cycle (16:49 09-15) — peer leads remain header-only/stub repetition; observability gap persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 16:49 09-15; 15+1 disclosure substance unchanged; auth map drift-free; no new primiti
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 01:19 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 12th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th consecutive triage cycle (09-16 05:15) consumed header-only/stub peer leads + nemotron3 reprint — observability ga
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root 200 CL:absent (was CL:0) persists at 01:19 09-16 — cosmetic header-shape shift only; 15+1 disclosure substance, 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 01:19 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 12th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 11th consecutive triage cycle (16:49 09-15) — peer leads remain header-only/stub repetition; observability gap persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists at 16:49 09-15; 15+1 disclosure substance unchanged; auth map drift-free; no new primiti
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 2.1MB inline tariff data (2,158,150 bytes) served unauthenticated, no-store+CF-DYNAMIC, no ETag/L
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 10th consecutive triage cycle (run-2026-09-14-22-17 "No leads provided"; peer state 33-byte stubs) — observability gap 

## RANKED HYPOTHESES 2026-09-16 11:58:17 UTC
- [89] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: hold — nothing before ≥01:19 09-17 (24h since 01:19 09-16 fragen.php 2,152,680 B measurement). At threshold, exactly one 1-rps GET, fresh jar:
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 01:19 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-16 16:40:20 UTC
- [89] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [89] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: hold — nothing before ≥01:19 09-17 (24h since 01:19 09-16 fragen.php 2,152,680 B measurement). At threshold, exactly one 1-rps GET, fresh jar:
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php — measure response time, confirm Content-Length ~2.1MB, extract Cache-Control/ETag/Last-Modified hea
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 01:19 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-16 20:04:45 UTC
- [89] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:19 09-17 (24h since 01:19 09-16 fragen.php 2,152,680 B measurement; now 19:46 09-16). At threshold, exactly one 1-rps GET https
- LEARN: REJECTED OTHER @ pipeline: 13th+ consecutive empty triage cycle (through 16:40 09-16 ranked block) — peer leads header-only/stub; observability gap persists, no
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed at 01:19 09-16 — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym

## RANKED HYPOTHESES 2026-09-16 22:50:47 UTC
- [89] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:19 09-17 (24h since 01:19 09-16 fragen.php 2,152,680 B measurement; now 20:04 09-16). At threshold, exactly one 1-rps GET https

## RANKED HYPOTHESES 2026-09-17 01:21:27 UTC
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:20 09-18 (24h since 2,152,680 B at 01:20 09-17). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_frag

## RANKED HYPOTHESES 2026-09-17 06:17:03 UTC
- [91] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: HOLD — 24h smoke window for fragen.php not yet met (last measurement 2026-09-16 16:38 UTC, 2,152,680 B). Next probe at ≥2026-09-17 16:38 UTC: exactly one
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-17 11:59:06 UTC
- [91] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:20 09-18 (24h since 2,152,680 B at 01:20 09-17). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_frag
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-17 16:38 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar; measure Content-Length, co
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-17 16:47:58 UTC
- [91] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:20 09-18 (24h since 2,152,680 B at 01:20 09-17). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_frag
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-17 16:38 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar; measure Content-Length, co
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 11:59 09-17 — 15/15 A/B, /sync/ HTTP-200 legacy, v2 middleware-A; root CL-absent 1167B pe
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed at 01:20 09-17 — 2,152,680 B (0.00% vs prior 25h), no caching mitigation; next r
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive empty triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attac
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-17 20:10:15 UTC
- [91] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥01:20 09-18 (24h since 2,152,680 B at 01:20 09-17). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_frag
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-17 20:08 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar; measure Content-Length, co
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle (through run-2026-09-17-18-50, peers laguna/ling3/longcat/mimo pure timestamp stubs, nemo
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 13th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf

## RANKED HYPOTHESES 2026-09-17 22:56:24 UTC
- [91] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 01:20 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 01:11:07 UTC
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 01:20 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 06:07:39 UTC
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 01:20 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live at 16:38 09-16 — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asym
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 11:37:09 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD — nothing before ≥11:30 09-19 (24h since 2,152,680 B at 11:30 09-18). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_frag
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 11:35 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 15:16:49 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- [90] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HOLD — nothing before ≥11:30 09-19 (24h since 2,152,680 B at 11:30 09-18). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php 
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 11:35 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed at 11:30 09-18 — 2,152,680 B (0.00% vs 01:20 09-17), no caching mitigation; drif
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length accurate again (was absent/CL:0 — cosmetic 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th+ consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surf
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 18:39:29 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 18:40 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 21:18:22 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HOLD — nothing before ≥11:30 09-19 (24h since 2,152,680 B at 11:30 09-18). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php 
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-18 18:40 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: auth map drift-free through 18:39 09-18 — 15/15 A/B map, /sync/ HTTP-200 legacy, v2 middleware-A gate, root 1167 B/15
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke proves drift-on-refresh model (2,152,680 B exact since 01:20 09-17); earlier "byte-stat
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th+ consecutive triage cycle consumed header-only/stub peer leads (laguna/ling3/longcat/mimo timestamps, nemotron3 re
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-18 23:30:14 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HOLD — nothing before ≥11:30 09-19 (24h since 2,152,680 B at 11:30 09-18). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php 
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root = 200, content-length 1167 == body 1167 B, 15 v1 ver 1.0 at 23:25 09-18 — header-shape continuity (CL accurate a
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B exact since 01:20 09-17 within ±0.3% window); next byte-rotati
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 15th+ consecutive triage cycle consumed empty/header-only peer leads (triage 09-11→22-21 all "No leads provided"; peers
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-19 01:38:28 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [90] www.kassenkompass.de/bonusrechner_fragen.php: Funnel Cookie Stuffing → device_id Anchored Lead State Bypass (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive empty triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs to 09-18 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: auth map drift-free through 23:25 09-18 — 15/15 A/B, /sync/ HTTP-200 legacy, v2 middleware-A, root 1167 B/15 v1 with accu
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-19 06:41:21 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HOLD — nothing before ≥11:30 09-19 UTC (24h since 2,152,680 B at 11:30 09-18; now 01:38). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusrech
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive empty triage cycle (through 01:38 09-19; laguna/ling3/longcat pure timestamp stubs, mimo "No leads pr
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: auth map drift-free through 23:25 09-18 — 15/15 A/B, /sync/ HTTP-200 legacy, v2 middleware-A, root 1167 B/15 v1 with accu
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-19 11:38:46 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Access via bonusrechner_fragen.php (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HOLD until ≥2026-09-19 11:30 UTC (24h since 2,152,680 B at 11:30 09-18; now ~06:45). At threshold: exactly one 1-rps GET https://kassenkompass.de/bonusre
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-19 14:55:03 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauth Tariff Database Scraping — 24h smoke verification (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh jar (no cookies/params); measure statu
- NEXT(hypotheses-nemotron3.txt): PROBE: At ≥2026-09-19 11:30 UTC execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measur
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED OTHER @ api.kassenkompass.de: auth map drift-free through 23:25 09-18 — 15/15 A/B, /sync/ HTTP-200 legacy, v2 middleware-A, root 1167 B/15 v1 with accu
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke passed — 2,152,680 B (+0.02% vs prior), no-store+CF-DYNAMIC, no caching mitigation; dri
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 14th consecutive triage cycle — peer leads header-only/stub; observability gap persists, no signal; no new attack surfa

## RANKED HYPOTHESES 2026-09-19 17:59:55 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauth Tariff Database Scraping — 24h smoke verification (iteration 3) (from art/lead_bigpickle.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥2026-09-20 17:55 UTC (24h since 2,152,708 B @17:54 09-19) execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh j
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measure Content-Length, confirm
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads

## RANKED HYPOTHESES 2026-09-19 20:27:29 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Unauthenticated Tariff Database Scraping — 24h smoke verification (iteration 4, mine) (from art/lead_bigpickle.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measure Content-Length, confirm
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads

## RANKED HYPOTHESES 2026-09-19 22:33:47 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [75] kassenkompass.de/bonusrechner_vergleich2.php: Mirror Doubles Tariff Leak Surface — www.kassenkompass.de Identical 2.1MB Exposure (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measure Content-Length, confirm
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh cookie jar (no cookies/params); measure Content-Length, confirm
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,680 B @11:30 09-18 → 2,152,708 B @23:25 09-18, +0.001%); next byte-r
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now absent (was CL:0) — same cosmetic class
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads

## RANKED HYPOTHESES 2026-09-20 00:26:14 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping — Rotation-6 Smoke (from art/lead_bigpickle.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥2026-09-20 22:33 UTC (24h since 2,152,708 B @22:33 09-19) execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh j
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke holds — 2,152,708 B @22:33 09-19 matches 23:25 09-18 measurement; drift-on-refresh with
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists through 22:33 09-19; 15+1 disclosure substance unchanged; auth map drift-free through 16
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal; no ne
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal; no new attack 

## RANKED HYPOTHESES 2026-09-20 05:28:10 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping — Rotation-6 Smoke (from art/lead_bigpickle.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥2026-09-20 22:33 UTC (24h since 2,152,708 B @22:33 09-19) execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh j
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke holds — 2,152,708 B @22:33 09-19 matches 23:25 09-18 measurement; drift-on-refresh with
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root CL:0-with-body persists through 22:33 09-19; 15+1 disclosure substance unchanged; auth map drift-free through 16
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal; no ne
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (through run-2026-09-19-00-36; laguna/ling3/longcat pure timestamp stubs, mimo "No leads
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal; no new attack 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal; no new attack 

## RANKED HYPOTHESES 2026-09-20 10:17:07 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal; no new attack 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads; observability gap persists, zero new signal; no new attack 
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle with header-only/stub leads (run-2026-09-20-07-01 empty, peers timestamp stubs); observa
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds at 2,152,708 B across 5 rotation windows (11:30 09-18 → 22:33 09-19) — drif
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-20 14:26:48 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping — Rotation-7 Smoke (held) (from art/lead_bigpickle.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: at ≥2026-09-20 22:33 UTC (24h since 2,152,708 B @22:33 09-19) execute exactly one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php with fresh j
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 16th+ consecutive triage cycle (run-2026-09-20-10-17) — peer leads header-only/stub; observability gap persists, zero n
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root content-length now accurate (1167 = body) at 10:10 09-20 — cosmetic header-shape drift (CL:0→absent→accurate) ac
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds at 2,152,708 B per 10:10 09-20; next rotation window ≥22:33 UTC 09-20 not y
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-20 17:36:52 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [75] kassenkompass.de/bonusrechner_vergleich2.php: Funnel Cookie Stuffing → device_id Anchored Lead State Bypass (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute sustained 1-rps scraping test on both hosts — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrech
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-20 19:49:07 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — held (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — scheduled 24h smoke at ≥2026-09-20 22:33 UTC: one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php (fresh jar, no params) then 
- NEXT(hypotheses-nemotron3.txt): WAIT: 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC 2026-09-20 (per 09-19 22:33 measurement at 2,152,708 B); current time 17:36 UTC — h
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: rotation window ≥22:33 UTC 09-20 correctly withheld at 17:36 — discipline prevents premature prob
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 17th+ consecutive triage cycle through run-2026-09-20-10-17 consumed header-only/stub peer leads — observability gap pe
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: root header-shape noise class (CL:0→absent→accurate 1167) not re-tested this cycle — cosmetic, disclosure substance c
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-20 22:22:30 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: Scheduled 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC 2026-09-20 (per 09-19 22:33 measurement at 2,152,708 B); current time 22
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-21 00:23:18 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke ≥2026-09-21 00:22 UTC: one 1-rps GET https://kassenkompass.de/bonusrechner_fragen.php (fresh jar, no params), 3 s later GE
- NEXT(hypotheses-nemotron3.txt): PROBE: Scheduled 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC 2026-09-20 (per 09-19 22:33 measurement at 2,152,708 B); current time 22
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-21 05:32:29 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Scheduled 24h smoke rotation window for bonusrechner_fragen.php opens ≥22:33 UTC 2026-09-20 (per 09-19 22:33 measurement at 2,152,708 B); current time 22
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute overdue 24h smoke rotation for bonusrechner_fragen.php — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.d
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-21 11:09:38 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — 24h smoke rotation window opens ≥2026-09-21 22:21 UTC (per 09-20 22:21 measurement at 2,152,708 B). At window: one 1-rps GET https://kass
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute overdue 24h smoke rotation for bonusrechner_fragen.php — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.d
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds at 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 17th+ consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no ne
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-21 17:09:33 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — 24h smoke rotation window opens ≥2026-09-21 22:21 UTC (per 09-20 22:21 measurement at 2,152,708 B). At window: one 1-rps GET https://kass
- NEXT(hypotheses-nemotron3.txt): PROBE: Execute overdue 24h smoke rotation for bonusrechner_fragen.php — GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.d
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 17th+ consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no ne
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-21 21:09:47 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — 24h smoke rotation window opens ≥2026-09-21 22:21 UTC (per 09-20 22:21 measurement at 2,152,708 B). At window: one 1-rps GET https://kass
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads (run-2026-09-21-18-48 empty; laguna/ling3/longcat pu
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds (2,152,708 B stable), no-store+CF-DYNAMIC, no ETag/Last-Modified, no rate l
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no

## RANKED HYPOTHESES 2026-09-22 00:18:51 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B measured 00:11 09-22). At window: one 1-rps GET https://
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 00:11 09-22 smoke — apex+www both 200 / 2,152,708 B exact, bodies differ by 1 byte (cfemail nonce
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th+ consecutive empty triage cycle (run-2026-09-21-18-48 "No leads provided"; laguna/ling3/longcat timestamp stubs, m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new

## RANKED HYPOTHESES 2026-09-22 05:10:49 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B measured 00:11 09-22). At window: one 1-rps GET https://
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 00:11 09-22 smoke — apex+www both 200 / 2,152,708 B exact, bodies differ by 1 byte (cfemail nonce
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th+ consecutive empty triage cycle (run-2026-09-21-18-48 "No leads provided"; laguna/ling3/longcat timestamp stubs, m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new

## RANKED HYPOTHESES 2026-09-22 10:07:49 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B measured 00:11 09-22). At window: one 1-rps GET https://
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 00:11 09-22 smoke — apex+www both 200 / 2,152,708 B exact, bodies differ by 1 byte (cfemail nonce
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th+ consecutive empty triage cycle — observability gap persists, zero new signal, no new attack surface anywhere.
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new

## RANKED HYPOTHESES 2026-09-22 15:08:55 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B measured 00:11 09-22). At window: one 1-rps GET https://
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 00:11 09-22 smoke — apex+www both 200 / 2,152,708 B exact, bodies differ by 1 byte (cfemail nonce
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th+ consecutive empty triage cycle (run-2026-09-21-18-48 "No leads provided"; laguna/ling3/longcat timestamp stubs, m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new

## RANKED HYPOTHESES 2026-09-22 19:02:50 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — next 24h smoke rotation window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B measured 00:11 09-22). At window: one 1-rps GET https://
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 19th consecutive triage cycle with header-only/stub peer leads (laguna/ling3/longcat timestamp stubs, mimo empty, nemot
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke discipline holds — 2,152,708 B byte-frozen across 4 consecutive windows (09-18→09-22), 
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 8+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length: 0 header with full body persists; catalog 
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18th consecutive triage cycle consumed header-only/stub peer leads; observability gap persists, zero new signal, no new

## RANKED HYPOTHESES 2026-09-22 22:02:50 UTC
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale — 2.1MB Competitive Intelligence Leak (from art/lead_nemotron3.txt)
- [92] kassenkompass.de/bonusrechner_fragen.php: Sustained Unauthenticated Tariff Database Scraping At Scale (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: DEFERRED-HOLD — window opens ≥2026-09-23 00:11 UTC (baseline 2,152,708 B @00:11 09-22; now 22:00Z 09-22, ~2h early). At window: one 1-rps GET https://kas
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://kassenkompass.de/bonusrechner_fragen.php and GET https://www.kassenkompass.de/bonusrechner_fragen.php alternating for 20 requests at 1 rps; m
- LEARN: ACCEPTED MISCONFIG @ kassenkompass.de/bonusrechner_fragen.php: 24h smoke model holds — 2,152,708 B across 9+ rotation windows (frozen since ~09-18, ±0.3% drift-
- LEARN: ACCEPTED MISCONFIG @ www.kassenkompass.de/bonusrechner_fragen.php: Identical 2,152,708 B payload, same headers — mirror surface doubled confirmed live
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: root disclosure stable — 1167 B, 15 v1 endpoints, ver 1.0; content-length now accurate (was 0); catalog disclosure wi
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error body instead of 401 — behavioral misconfiguration persists
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages — "ungültig oder nicht berechtigt" (8 endpoints + v2) vs "Ungültiger X-API-Secret" (o
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de/v2: greedy segment match confirmed — /v2/insurance_info/1/extra reaches auth handler (401); kk_id not validated at rou
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner.php: stuffing mirror re-confirmed live — lizenz/jid/agn/ppn→4 1yr cookies exact, attribute asymmetry intact (a
- LEARN: ACCEPTED OTHER @ kassenkompass.de/bonusrechner_vergleich2.php: device_id cookie (1yr Secure HttpOnly SameSite=Lax) + catoint force-deleted — sole funnel step em
- LEARN: ACCEPTED BUSLOGIC @ kassenkompass.de/bonusrechner_abschluss.php: GET vs POST differential — "Account-ID nicht gefunden" present ONLY on POST; server validates A
- LEARN: REJECTED AUTH @ api.kassenkompass.de: query-string AND cookie X-API-Secret both return missing-header 401 on A/B/v2 — header strictly sole channel; source-merge
- LEARN: ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map 15/15 complete — /cancel/{id} joins middleware B; B = kk_webapp-delegation stack {user, cancel}; v2 shares m
- LEARN: REJECTED MISCONFIG @ api.kassenkompass.de: No new enumeration primitive — v2 oracle saturated at 42 names, auth source-merge closed, format-side differential no
- LEARN: REJECTED OTHER @ kassenkompass pipeline: 18+ consecutive triage cycles consumed header-only/stub peer leads; observability gap persists, zero new signal, no new
