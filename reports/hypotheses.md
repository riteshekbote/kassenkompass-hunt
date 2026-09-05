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
