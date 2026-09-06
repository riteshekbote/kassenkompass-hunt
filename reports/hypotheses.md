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
