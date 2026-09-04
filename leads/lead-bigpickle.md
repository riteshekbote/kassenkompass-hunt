## 2026-09-03 17:18:57 UTC [target] (model bigpickle)
[NEW] api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
[NEW] kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
[NEW] www.kassenkompass.de — mirrors kassenkompass.de
[CHANGED] Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
[PRIO] api.kassenkompass.de,8.85,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=9
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} accepts ext_id path parameter, described as "Userdaten abrufen" (retrieve user data). Endpoint requires X-API-Secret but no indication of user-scoping or ownership check within the secret's authorization boundary. If the API secret is a global/shared key (common in MVP APIs), any valid secret could query any user by ext_id. The ext_id naming (external ID) suggests an incrementing or enumerable identifier from a connected system.
evidence_needed: HTTP response body from GET /user/{ext_id} with sequential ext_id values (1,2,3...) under a valid API secret to confirm PII exposure across users.
verify_steps: PASSIVE: None - requires API secret (auth_helped). WITH AUTH: GET /user/1, GET /user/2, GET /user/3 with valid X-API-Secret header; compare response bodies for different users.
impact: Attacker with valid API secret reads any user's personal data (PII: name, insurance, email, address). Severity: HIGH (GDPR-relevant PII breach).
testability: AUTH_HELPED
[HYP] IDOR on /delete/{id} - unauthorized user data deletion
class: IDOR
asset: api.kassenkompass.de
confidence: 55
reasoning: DELETE /delete/{id} accepts numeric id parameter, described as "Benutzerdaten löschen" (delete user data). Same X-API-Secret auth as other endpoints. If auth is a global key, any caller can delete any user's data. This is a destructive endpoint without apparent ownership verification.
evidence_needed: Response from DELETE /delete/{id} with different id values under a valid API secret; confirm 200/204 vs 403/404 for different users.
verify_steps: WITH AUTH: DELETE /delete/1 with valid X-API-Secret; observe status code and body. Repeat with sequential ids.
impact: Attacker with valid API secret mass-deletes user accounts/data. Severity: HIGH (data integrity destruction).
testability: AUTH_HELPED
[HYP] Unauthenticated API documentation disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any path on api.kassenkompass.de returns the full API documentation JSON including endpoint map, descriptions, version info, and auth requirements — no auth needed. Paths tested: /, /admin/, /debug/, /docs/, /swagger/, /openapi.json, /api/, /robots.txt. The catch-all route handler returns the same JSON regardless of path. This reveals the full API surface to any unauthenticated scanner.
evidence_needed: Already confirmed via GET /api.kassenkompass.de/ (returns full endpoint map).
verify_steps: PASSIVE: GET /nonexistent-path-12345 — confirm same JSON response. Done.
impact: Attacker maps complete API surface without auth, enabling targeted attacks on /user/{ext_id}, /delete/{id}, /cancel/{id}. Severity: LOW-MEDIUM (information disclosure enabling further attack).
testability: PASSIVE
[FINAL] 1. Unauthenticated API docs disclosure (MISCONFIG, 88)
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62)
[FINAL] 3. IDOR on /delete/{id} (IDOR, 55)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with no auth header — confirm whether /user/{ext_id} returns data or clean 401 (the sync endpoint returned a structured JSON error `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` so different endpoints may have different unauth behavior). Then GET https://api.kassenkompass.de/user/100 to compare.
[RISK] kassenkompass: 35/100. API auth gate limits passive-only findings; no public source code for deeper analysis; Cloudflare WAF fronting adds defense layer. Main value is in auth-helped IDOR testing on api.kassenkompass.de.
## 2026-09-03 20:02:44 UTC [target] (model bigpickle)
[NEW] `/sync/` returns HTTP 200 + auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401, not 200)
[NEW] `/health/` confirmed unprotected, returns `{"status":"ok"}` + PHP version disclosure (`x-powered-by: PHP/8.4.3`)
[NEW] All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
[NEW] Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
[NEW] `/insurance_info/{kk_id}` returns proper RFC 9457 401 error (unlike `/sync/`), confirming inconsistent error handling across endpoints
[NEW] No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
[CHANGED] API catalog confirmed 15 endpoints; `/health/` is only fully unprotected endpoint
[PRIO] api.kassenkompass.de,8.85,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=9
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} accepts ext_id path parameter, described as "Userdaten abrufen" (retrieve user data). Endpoint requires X-API-Secret but no indication of user-scoping or ownership check within the secret's authorization boundary. If the API secret is a global/shared key (common in MVP APIs), any valid secret could query any user by ext_id. The ext_id naming (external ID) suggests an incrementing or enumerable identifier from a connected system. Unauth test returned 401 (confirmed auth gate), but auth boundary is unknown without valid key.
evidence_needed: HTTP response body from GET /user/{ext_id} with sequential ext_id values (1,2,3...) under a valid API secret to confirm PII exposure across users.
verify_steps: PASSIVE: None - requires API secret (auth_helped). WITH AUTH: GET /user/1, GET /user/2, GET /user/3 with valid X-API-Secret header; compare response bodies for different users.
impact: Attacker with valid API secret reads any user's personal data (PII: name, insurance, email, address). Severity: HIGH (GDPR-relevant PII breach).
testability: AUTH_HELPED
[HYP] Missing CSRF tokens on all login and password-reset forms enable session fixation via cross-site request
class: AUTH
asset: kassenkompass.de
confidence: 65
reasoning: All four forms (/login_kd.php, /login_kk.php, /login_partner.php, /pw_reset_partner.php) use POST with no CSRF token in the form body or as a cookie-based token. An attacker can craft a page that auto-submits a POST with victim's email/password if they can intercept credentials via a MITM on the same origin (no SameSite on cookies is unconfirmed). The "Eingeloggt bleiben" (remember me) checkbox on customer and partner logins increases session persistence risk. The client-side-only validation (email length >= 3) provides no server-side CSRF mitigation.
evidence_needed: Confirm Set-Cookie lacks SameSite attribute on login response; confirm session cookie is not HttpOnly; test if POST /login_kd.php from cross-origin accepts valid credentials.
verify_steps: PASSIVE: Already confirmed no CSRF token in form HTML. WITH AUTH: POST login_kd.php with valid credentials and observe Set-Cookie headers; check SameSite attribute.
impact: Attacker tricks victim into visiting a page that auto-submits login form, potentially performing account takeover or session fixation. Severity: MEDIUM (requires social engineering but enables credential theft).
testability: AUTH_HELPED
[HYP] Unprotected API documentation disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any path on api.kassenkompass.de returns the full API documentation JSON including 15 endpoint descriptions, version info, and auth requirements — no auth needed. Confirmed paths: /, /admin/, /debug/, /swagger/, /openapi.json. This reveals the complete attack surface including /user/{ext_id}, /delete/{id}, /cancel/{id}, and /settlement_report/{year}/{month}.
evidence_needed: Already confirmed via GET / (returns full endpoint map).
verify_steps: PASSIVE: GET /nonexistent-path-12345 — confirm same JSON response. Done.
impact: Attacker maps complete API surface without auth, enabling targeted attacks on sensitive endpoints. Severity: LOW-MEDIUM (information disclosure enabling further attack).
testability: PASSIVE
[PARKED] IDOR on /delete/{id}: confidence 55, destructive endpoint — no safe passive verification, requires valid API key; park until key is obtained.
[PARKED] Missing CSRF tokens on login forms: confidence 65, AUTH_HELPED — requires valid session cookie to confirm SameSite behavior; edge case where impact depends on cookie flags.
[FINAL] 1. Unauthenticated API docs disclosure (MISCONFIG, 88) — PASSIVE, already confirmed
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid API key
[FINAL] 3. Missing CSRF tokens on login forms (AUTH, 65) — AUTH_HELPED, needs cookie analysis
[NEXT] PROBE: GET https://api.kassenkompass.de/sync/ -H "X-API-Secret: test" — test if sending any value in X-API-Secret header causes /sync/ to return different data or 200 vs 401; compare with a random invalid key to confirm auth enforcement (read-only GET, no data mutation).
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners.
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified.
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable.
[RISK] kassenkompass: 38/100. API auth gate consistently enforced (401 on all data endpoints), limiting passive-only findings; main value is in auth-helped IDOR testing on api.kassenkompass.de once API key is obtained; frontend login forms lack CSRF tokens but require social engineering; Cloudflare WAF fronting adds defense layer; PHP 8.4.3 backend disclosed via x-powered-by header.
## 2026-09-03 22:31:24 UTC [target] (model bigpickle)
[NEW] api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
[NEW] kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
[NEW] www.kassenkompass.de — mirrors kassenkompass.de
[CHANGED] Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
[PRIO] api.kassenkompass.de,8.85,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=9
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} accepts ext_id path parameter, described as "Userdaten abrufen" (retrieve user data). Endpoint requires X-API-Secret but no indication of user-scoping or ownership check within the secret's authorization boundary. If the API secret is a global/shared key (common in MVP APIs), any valid secret could query any user by ext_id. The ext_id naming (external ID) suggests an incrementing or enumerable identifier from a connected system.
evidence_needed: HTTP response body from GET /user/{ext_id} with sequential ext_id values (1,2,3...) under a valid API secret to confirm PII exposure across users.
verify_steps: PASSIVE: None - requires API secret (auth_helped). WITH AUTH: GET /user/1, GET /user/2, GET /user/3 with valid X-API-Secret header; compare response bodies for different users.
impact: Attacker with valid API secret reads any user's personal data (PII: name, insurance, email, address). Severity: HIGH (GDPR-relevant PII breach).
testability: AUTH_HELPED
[HYP] IDOR on /delete/{id} - unauthorized user data deletion
class: IDOR
asset: api.kassenkompass.de
confidence: 55
reasoning: DELETE /delete/{id} accepts numeric id parameter, described as "Benutzerdaten löschen" (delete user data). Same X-API-Secret auth as other endpoints. If auth is a global key, any caller can delete any user's data. This is a destructive endpoint without apparent ownership verification.
evidence_needed: Response from DELETE /delete/{id} with different id values under a valid API secret; confirm 200/204 vs 403/404 for different users.
verify_steps: WITH AUTH: DELETE /delete/1 with valid X-API-Secret; observe status code and body. Repeat with sequential ids.
impact: Attacker with valid API secret mass-deletes user accounts/data. Severity: HIGH (data integrity destruction).
testability: AUTH_HELPED
[HYP] Unauthenticated API documentation disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any path on api.kassenkompass.de returns the full API documentation JSON including endpoint map, descriptions, version info, and auth requirements — no auth needed. Paths tested: /, /admin/, /debug/, /docs/, /swagger/, /openapi.json, /api/, /robots.txt. The catch-all route handler returns the same JSON regardless of path. This reveals the full API surface to any unauthenticated scanner.
evidence_needed: Already confirmed via GET /api.kassenkompass.de/ (returns full endpoint map).
verify_steps: PASSIVE: GET /nonexistent-path-12345 — confirm same JSON response. Done.
impact: Attacker maps complete API surface without auth, enabling targeted attacks on /user/{ext_id}, /delete/{id}, /cancel/{id}. Severity: LOW-MEDIUM (information disclosure enabling further attack).
testability: PASSIVE
[FINAL] 1. Unauthenticated API docs disclosure (MISCONFIG, 88)
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62)
[FINAL] 3. IDOR on /delete/{id} (IDOR, 55)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with no auth header — confirm whether /user/{ext_id} returns data or clean 401 (the sync endpoint returned a structured JSON error `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` so different endpoints may have different unauth behavior). Then GET https://api.kassenkompass.de/user/100 to compare.
[RISK] kassenkompass: 35/100. API auth gate limits passive-only findings; no public source code for deeper analysis; Cloudflare WAF fronting adds defense layer. Main value is in auth-helped IDOR testing on api.kassenkompass.de.
[NEW] `/sync/` returns HTTP 200 + auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401, not 200)
[NEW] `/health/` confirmed unprotected, returns `{"status":"ok"}` + PHP version disclosure (`x-powered-by: PHP/8.4.3`)
[NEW] All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
[NEW] Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
[NEW] `/insurance_info/{kk_id}` returns proper RFC 9457 401 error (unlike `/sync/`), confirming inconsistent error handling across endpoints
[NEW] No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
[CHANGED] API catalog confirmed 15 endpoints; `/health/` is only fully unprotected endpoint
[PRIO] api.kassenkompass.de,8.85,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=9
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} accepts ext_id path parameter, described as "Userdaten abrufen" (retrieve user data). Endpoint requires X-API-Secret but no indication of user-scoping or ownership check within the secret's authorization boundary. If the API secret is a global/shared key (common in MVP APIs), any valid secret could query any user by ext_id. The ext_id naming (external ID) suggests an incrementing or enumerable identifier from a connected system. Unauth test returned 401 (confirmed auth gate), but auth boundary is unknown without valid key.
evidence_needed: HTTP response body from GET /user/{ext_id} with sequential ext_id values (1,2,3...) under a valid API secret to confirm PII exposure across users.
verify_steps: PASSIVE: None - requires API secret (auth_helped). WITH AUTH: GET /user/1, GET /user/2, GET /user/3 with valid X-API-Secret header; compare response bodies for different users.
impact: Attacker with valid API secret reads any user's personal data (PII: name, insurance, email, address). Severity: HIGH (GDPR-relevant PII breach).
testability: AUTH_HELPED
[HYP] Missing CSRF tokens on all login and password-reset forms enable session fixation via cross-site request
class: AUTH
asset: kassenkompass.de
confidence: 65
reasoning: All four forms (/login_kd.php, /login_kk.php, /login_partner.php, /pw_reset_partner.php) use POST with no CSRF token in the form body or as a cookie-based token. An attacker can craft a page that auto-submits a POST with victim's email/password if they can intercept credentials via a MITM on the same origin (no SameSite on cookies is unconfirmed). The "Eingeloggt bleiben" (remember me) checkbox on customer and partner logins increases session persistence risk. The client-side-only validation (email length >= 3) provides no server-side CSRF mitigation.
evidence_needed: Confirm Set-Cookie lacks SameSite attribute on login response; confirm session cookie is not HttpOnly; test if POST /login_kd.php from cross-origin accepts valid credentials.
verify_steps: PASSIVE: Already confirmed no CSRF token in form HTML. WITH AUTH: POST login_kd.php with valid credentials and observe Set-Cookie headers; check SameSite attribute.
impact: Attacker tricks victim into visiting a page that auto-submits login form, potentially performing account takeover or session fixation. Severity: MEDIUM (requires social engineering but enables credential theft).
testability: AUTH_HELPED
[HYP] Unprotected API documentation disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any path on api.kassenkompass.de returns the full API documentation JSON including 15 endpoint descriptions, version info, and auth requirements — no auth needed. Confirmed paths: /, /admin/, /debug/, /swagger/, /openapi.json. This reveals the complete attack surface including /user/{ext_id}, /delete/{id}, /cancel/{id}, and /settlement_report/{year}/{month}.
evidence_needed: Already confirmed via GET / (returns full endpoint map).
verify_steps: PASSIVE: GET /nonexistent-path-12345 — confirm same JSON response. Done.
impact: Attacker maps complete API surface without auth, enabling targeted attacks on sensitive endpoints. Severity: LOW-MEDIUM (information disclosure enabling further attack).
testability: PASSIVE
[PARKED] IDOR on /delete/{id}: confidence 55, destructive endpoint — no safe passive verification, requires valid API key; park until key is obtained.
[PARKED] Missing CSRF tokens on login forms: confidence 65, AUTH_HELPED — requires valid session cookie to confirm SameSite behavior; edge case where impact depends on cookie flags.
[FINAL] 1. Unauthenticated API docs disclosure (MISCONFIG, 88) — PASSIVE, already confirmed
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid API key
[FINAL] 3. Missing CSRF tokens on login forms (AUTH, 65) — AUTH_HELPED, needs cookie analysis
[NEXT] PROBE: GET https://api.kassenkompass.de/sync/ -H "X-API-Secret: test" — test if sending any value in X-API-Secret header causes /sync/ to return different data or 200 vs 401; compare with a random invalid key to confirm auth enforcement (read-only GET, no data mutation).
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners.
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified.
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable.
[RISK] kassenkompass: 38/100. API auth gate consistently enforced (401 on all data endpoints), limiting passive-only findings; main value is in auth-helped IDOR testing on api.kassenkompass.de once API key is obtained; frontend login forms lack CSRF tokens but require social engineering; Cloudflare WAF fronting adds defense layer; PHP 8.4.3 backend disclosed via x-powered-by header.
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: GET / returns complete endpoint list including sensitive endpoints (/user/{ext_id}, /delete/{id}, /settlement_report/{year}/{month}, /cancel/{id}) without any authentication; this is excessive information disclosure that maps the attack surface for auth-bypass/IDOR attempts
evidence_needed: Confirm endpoint list matches actual implemented endpoints; verify no rate-limiting on catalog endpoint
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 14 endpoints respond
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance time from hours to seconds; HIGH if any endpoint has auth flaw
testability: PASSIVE
[HYP] User Data Access via /user/{ext_id} IDOR/BOLA After Auth Acquisition
class: IDOR
asset: api.kassenkompass.de
confidence: 65
reasoning: Endpoint `/user/{ext_id}` explicitly returns "Userdaten abrufen" per catalog; ext_id likely external user identifier (predictable/sequential); if X-API-Secret is obtainable (leak, weak generation, partner compromise) or authz check missing, cross-user data access possible
evidence_needed: Valid X-API-Secret to test authorization enforcement across ext_id values; or evidence of secret leakage in client code/GitHub/logs
verify_steps: Obtain valid X-API-Secret (partner/insurer flow); GET /user/1, /user/2, /user/999999 with valid secret; compare responses for data isolation
impact: Cross-tenant PII dump (health insurance data, personal info, financial); HIGH/CRITICAL
testability: AUTH_HELPED
[HYP] Settlement Report Endpoint Exposes Financial Data via BOLA
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 60
reasoning: `/settlement_report/{year}/{month}` returns "Abrechnungs-Report (Cassatis Prime, CSV-Download bzw. /json)" - financial settlement data; if authz missing or weak (e.g., partner can access other partners' reports), mass financial data exposure
evidence_needed: Valid X-API-Secret with partner/insurer scope; test access to reports for different year/month combos and cross-account access
verify_steps: With valid partner/insurer secret: GET /settlement_report/2024/01, /settlement_report/2023/12; attempt to access other tenant IDs if parameter exists
impact: Financial/commission data leakage across insurers/partners; HIGH
testability: AUTH_HELPED
[PARKED] User Data Access via /user/{ext_id} IDOR/BOLA After Auth Acquisition: confidence 65 but requires valid X-API-Secret (AUTH_HELPED) - no passive path to obtain secret; cannot verify without partner/insurer cooperation
[PARKED] Settlement Report Endpoint Exposes Financial Data via BOLA: confidence 60 but same AUTH_HELPED limitation; requires valid scoped secret
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE) — **TOP PRIORITY**
[NEXT] PROBE: GET https://api.kassenkompass.de/delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] BOLA on /delete/{id} — authenticated arbitrary resource deletion
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 70
reasoning: Catalog exposes `/delete/{id}` as "Löschen" (destructive); X-API-Secret auth is single-header; no evidence of resource-level authorization in catalog; if authz checks only validate header presence not resource ownership, any valid secret deletes any ID
evidence_needed: Valid X-API-Secret to test cross-resource deletion; or evidence that secret scope is not resource-bound
verify_steps: GET https://api.kassenkompass.de/delete/1 (no auth → expect 401); with valid secret: GET /delete/1, /delete/2, /delete/999999 — compare responses for authz enforcement
impact: Authenticated user deletes other users'/partners' records (settlements, user data, configs); HIGH
testability: AUTH_HELPED
[HYP] OAuth redirect_uri validation bypass across multi-tenant login portals
class: OATH
asset: kassenkompass.de
confidence: 55
reasoning: Three distinct login portals (customer/partner/insurer) on same domain; common pattern: shared OAuth/SSO implementation with weak redirect_uri allowlist (subdomain/wildcard) enabling code theft via open redirect or subdomain takeover
evidence_needed: OAuth authorize endpoint location; redirect_uri parameter handling; allowlist configuration
verify_steps: GET https://kassenkompass.de/login (identify OAuth flow); GET /authorize?redirect_uri=https://evil.com — check validation; test subdomain wildcard (partner.kassenkompass.de, insurer.kassenkompass.de)
impact: Account takeover via authorization code theft across all three portal types; CRITICAL
testability: PASSIVE
[PARKED] BOLA on /delete/{id} — authenticated arbitrary resource deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] OAuth redirect_uri validation bypass across multi-tenant login portals: confidence 55 but needs manual portal interaction to map OAuth endpoints; no automated passive verification
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE) — from prior leads, remains highest-confidence verified finding
[NEXT] PROBE: GET https://api.kassenkompass.delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
[HYP] No candidate repositories identified for audit
class: OTHER
asset: n/a
confidence: 100
reasoning: cands.txt contains "no org candidates"; scope.yml lists github_orgs: "none-configured"
impact: N/A
verify_steps: N/A - no repos to scan
[HYP] Unauthenticated API documentation catalog at catch-all routes (confirmed)
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any path (/, /admin/, /debug/, /swagger/, /openapi.json, /user/1, /nonexistent) returns full 15-endpoint JSON catalog with descriptions, version and auth requirements — zero auth. Reconfirmed again this session via GET / (15 endpoints incl /delete/{id}, /cancel/{id}, /settlement_report/{year}/{month}).
evidence_needed: Already confirmed; catalog returned at every tested path.
verify_steps: PASSIVE: GET /, /debug/, /settlement_report/2026/9 (read-only header/shape check). Done.
impact: Attacker maps complete API attack surface without auth; enables targeted IDOR/BOLA planning against sensitive user-data/financial endpoints. Severity: LOW-MEDIUM.
testability: PASSIVE
[HYP] IDOR/BOLA on /user/{ext_id} — cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} returns "Userdaten abrufen"; ext_id is external, likely enumerable. Single shared X-API-Secret header with no visible resource scoping in catalog. Secret gate enforced (invalid vs missing distinct), so requires a valid secret; auth boundary across ext_id untested.
evidence_needed: Valid X-API-Secret; GET /user/1 vs /user/2 produce different user PII.
verify_steps: WITH AUTH: GET /user/1, /user/2 with valid secret; compare bodies.
impact: Attacker with valid secret reads any user's PII (name, insurance, email, address) — GDPR-relevant. Severity: HIGH.
testability: AUTH_HELPED
[HYP] BOLA on /settlement_report/{year}/{month} — cross-tenant financial data
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 60
reasoning: Endpoint returns financial settlement reports (CSV/json) via X-API-Secret only; no evidence report access is scoped to the secret's partner/insurer tenant. If authz only checks header validity, any valid secret retrieves any tenant's report for any year/month.
evidence_needed: Valid X-API-Secret; GET /settlement_report/2025/01 for other tenants differs.
verify_steps: WITH AUTH: GET /settlement_report/2024/01, /2023/12 with valid secret; observe cross-tenant data.
impact: Attacker with valid secret exfiltrates financial/commission settlement data across partners/insurers. Severity: HIGH.
testability: AUTH_HELPED
[NEW] `/sync/` with ANY supplied X-API-Secret value returns distinct body `"Ungültiger X-API-Secret"` (invalid) vs `"fehlt"` (missing) — gate genuinely enforced, not bypassable by header presence
[NEW] Partner password-reset magic `KKX3382745` does NOT authenticate as API secret (returns "Ungültiger") — no cross-asset credential reuse
[NEW] No access-control-allow-origin reflection for arbitrary Origin on api — CORS misconfig REJECTED
[NEW] `/post/` also requires X-API-Secret; GET/OPTIONS reveal no bypass
[CHANGED] All API data endpoints remain auth-gated; no egress to AUTH_HELPED hypotheses this session
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=8
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} returns "Userdaten abrufen"; ext_id external/enumerable; single shared X-API-Secret with no visible resource scoping in catalog. Secret gate enforced (invalid vs missing distinct), so requires valid secret; cross ext_id authz untested.
evidence_needed: Valid X-API-Secret; GET /user/1 vs /user/2 produce different PII.
verify_steps: WITH AUTH: GET /user/1, /user/2 with valid secret; compare bodies.
impact: Attacker with valid secret reads any user's PII (name, insurance, email, address) — GDPR-relevant. Severity: HIGH.
testability: AUTH_HELPED
[HYP] BOLA on /settlement_report/{year}/{month} - cross-tenant financial data
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 60
reasoning: Endpoint returns financial settlement reports via X-API-Secret only; no evidence report access is scoped to secret's tenant. If authz only validates header, any valid secret retrieves any tenant report.
evidence_needed: Valid X-API-Secret; GET /settlement_report/2025/01 for other tenants differs.
verify_steps: WITH AUTH: GET /settlement_report/2024/01, /2023/12 with valid secret; observe cross-tenant data.
impact: Financial/commission settlement data exfiltration across partners/insurers. Severity: HIGH.
testability: AUTH_HELPED
[HYP] Unauthenticated API catalog disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any tested path (/, /admin/, /debug/, /swagger/, /openapi.json, /nonexistent) returns full 15-endpoint catalog JSON with no auth. Reconfirmed this session via GET /.
evidence_needed: Already confirmed.
verify_steps: PASSIVE: GET /, /debug/, /settlement_report/9999/13. Done.
impact: Complete API attack surface disclosed; enables targeted IDOR/BOLA planning. Severity: LOW-MEDIUM.
testability: PASSIVE
[PARKED] IDOR on /user/{ext_id}: 62, AUTH_HELPED, no passive secret path — park until valid key obtained
[PARKED] BOLA on /delete//cancel/{id}: destructive, AUTH_HELPED, no safe verification — park until key obtained
[PARKED] BOLA /settlement_report: 60, AUTH_HELPED, needs valid scoped secret
[PARKED] CSRF on login forms: anonymous-form CSRF is program-out-of-scope; weak — parked
[FINAL] 1. Unauthenticated API catalog disclosure (MISCONFIG, 88) — PASSIVE, verified
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid key
[FINAL] 3. BOLA on /settlement_report (BUSLOGIC, 60) — AUTH_HELPED, needs valid scoped key
[NEXT] PROBE: GET https://api.kassenkompass.de/settlement_report/9999/13 — read-only, confirm error shape/behavior for financial endpoint under invalid auth (no mutation). Broader unlock: obtain valid X-API-Secret to test IDOR/BOLA on /user/, /delete/, /cancel/, /settlement_report.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root/catch-all discloses full 15-endpoint catalog without auth — least-privilege violation, recon amplifier.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Data endpoints return HTTP 200 + auth-error body instead of 401 — scanner-bypass behavior.
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT.
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins.
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret.
[RISK] kassenkompass: 38/100. API auth gate genuinely enforced across all data endpoints (invalid-vs-missing distinction, no header-presence bypass, no CORS reflection); only /health/ unprotected. High-value IDOR/BOLA gated behind single shared X-API-Secret — value is AUTH_HELPED, no passive egress found; partner magic value not reusable; Cloudflare + PHP 8.4.3; no source code; reposcan N/A.
## 2026-09-04 00:29:04 UTC [target] (model bigpickle)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=8
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} returns "Userdaten abrufen"; ext_id external/enumerable; single shared X-API-Secret with no visible resource scoping in catalog. Secret gate enforced (invalid vs missing distinct), so requires valid secret; cross ext_id authz untested.
evidence_needed: Valid X-API-Secret; GET /user/1 vs /user/2 produce different PII.
verify_steps: WITH AUTH: GET /user/1, /user/2 with valid secret; compare bodies.
impact: Attacker with valid secret reads any user's PII (name, insurance, email, address) — GDPR-relevant. Severity: HIGH.
testability: AUTH_HELPED
[HYP] BOLA on /settlement_report/{year}/{month} - cross-tenant financial data
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 60
reasoning: Endpoint returns financial settlement reports (CSV/json) via X-API-Secret only; no evidence report access is scoped to the secret's partner/insurer tenant. If authz only checks header validity, any valid secret retrieves any tenant's report for any year/month.
evidence_needed: Valid X-API-Secret; GET /settlement_report/2025/01 for other tenants differs.
verify_steps: WITH AUTH: GET /settlement_report/2024/01, /settlement_report/2023/12 with valid secret; observe cross-tenant data.
impact: Attacker with valid secret exfiltrates financial/commission settlement data across partners/insurers. Severity: HIGH.
testability: AUTH_HELPED
[HYP] Unauthenticated API catalog disclosure at catch-all routes
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 88
reasoning: Any tested path (/, /admin/, /debug/, /swagger/, /openapi.json, /nonexistent) returns full 15-endpoint catalog JSON with no auth. Reconfirmed this session via GET /.
evidence_needed: Already confirmed.
verify_steps: PASSIVE: GET /, /debug/, /settlement_report/9999/13. Done.
impact: Complete API attack surface disclosed; enables targeted IDOR/BOLA planning. Severity: LOW-MEDIUM.
testability: PASSIVE
[PARKED] IDOR on /user/{ext_id}: 62, AUTH_HELPED, no passive secret path — park until valid key obtained
[PARKED] BOLA on /delete//cancel/{id}: destructive, AUTH_HELPED, no safe verification — park until key obtained
[PARKED] BOLA /settlement_report: 60, AUTH_HELPED, needs valid scoped secret
[PARKED] CSRF on login forms: anonymous-form CSRF is program-out-of-scope; weak — parked
[FINAL] 1. Unauthenticated API catalog disclosure (MISCONFIG, 88) — PASSIVE, verified
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid key
[FINAL] 3. BOLA on /settlement_report (BUSLOGIC, 60) — AUTH_HELPED, needs valid scoped key
[NEXT] PROBE: GET https://api.kassenkompass.de/settlement_report/9999/13 — read-only, confirm error shape/behavior for financial endpoint under invalid auth (no mutation). Broader unlock: obtain valid X-API-Secret to test IDOR/BOLA on /user/, /delete/, /cancel/, /settlement_report.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root/catch-all discloses full 15-endpoint catalog without auth — least-privilege violation, recon amplifier.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Data endpoints return HTTP 200 + auth-error body instead of 401 — scanner-bypass behavior.
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT.
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins.
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret.
[RISK] kassenkompass: 38/100. API auth gate genuinely enforced across all data endpoints (invalid-vs-missing distinction, no header-presence bypass, no CORS reflection); only /health/ unprotected. High-value IDOR/BOLA gated behind single shared X-API-Secret — value is AUTH_HELPED, no passive egress found; partner magic value not reusable; Cloudflare + PHP 8.4.3; no source code; reposcan N/A.
## 2026-09-04 05:09:08 UTC [target] (model bigpickle)
[NEW] Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — suggests two separate auth middleware paths
[NEW] `/cat_detail/` catalog advertises GET but actually requires POST (returns 405 for GET) — catalog discrepancy
[CHANGED] `/settlement_report/9999/13` confirmed: 401 (no auth) / 403 (invalid auth) — proper RFC 9457 format, consistent with majority of endpoints
[CHANGED] `/sync/` remains sole endpoint returning HTTP 200 with auth error body (known MISCONFIG)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=8
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] Two-tier auth middleware exposes differential authorization paths — BOLA/endpoint-scoping bypass potential
class: AUTH
asset: api.kassenkompass.de
confidence: 55
reasoning: Two distinct 403 messages detected: (A) "Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt" on /settlement_report/, /question_tree/, /health_insurance/, /health_insurance_savings/, /health_insurance_comparison/, /detail_comparison/, /state/, /insurance_info/{kk_id} (8 endpoints); (B) "Ungültiger X-API-Secret" on /user/{ext_id} only. /sync/ uses yet a third path (HTTP 200 + error body). Three different error handlers across 15 endpoints indicates separate auth middleware classes/stacks. If a valid secret passes middleware A but the authorization scope check is only in middleware B (or vice versa), cross-endpoint access may differ.
evidence_needed: Valid X-API-Secret tested against both middleware groups; whether a secret valid for group A works on group B endpoints.
verify_steps: WITH AUTH: test valid secret against /user/1 (group B) vs /health_insurance/ (group A); compare 200 vs 403 response shapes. PASSIVE: No additional passive verification possible.
impact: If middleware groups enforce different authorization scopes, a secret scoped to read endpoints (group A) might bypass authorization on /user/{ext_id} (group B) or vice versa — cross-tenant PII or financial data access. Severity: HIGH (depends on actual scoping).
testability: AUTH_HELPED
[HYP] API catalog discrepancy on /cat_detail/ — method mismatch reveals undocumented POST endpoint
class: MISCONFIG
asset: api.kassenkompass.de/cat_detail/
confidence: 42
reasoning: Catalog at root lists "GET /cat_detail/" as an endpoint. Actual behavior: GET returns 405 "GET-Methode ist für diesen Endpunkt nicht erlaubt. Bitte verwenden Sie POST." The catalog is inaccurate — the endpoint requires POST. POST with empty body returns 401 (auth required). OPTIONS returns 200. This indicates undocumented data-submission endpoint whose request schema is unknown.
evidence_needed: POST body schema for /cat_detail/ with valid auth; whether it accepts arbitrary/overly-broad parameters.
verify_steps: WITH AUTH: POST /cat_detail/ with empty body, then with {"kk_id":"1"}, observe response. PASSIVE: Already confirmed catalog mismatch.
impact: Undocumented POST endpoint may accept broader parameters than intended, potentially enabling excessive data retrieval or parameter injection. Severity: LOW-MEDIUM (speculative without schema).
testability: AUTH_HELPED
[HYP] IDOR on /user/{ext_id} - cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} returns "Userdaten abrufen"; ext_id is external/enumerable; single shared X-API-Secret with no visible resource scoping in catalog. The endpoint uses a distinct auth middleware (message B) from most other endpoints — if authorization is not per-resource, any valid secret reads any user.
evidence_needed: Valid X-API-Secret; GET /user/1 vs /user/2 produce different PII.
verify_steps: WITH AUTH: GET /user/1, /user/2 with valid secret; compare bodies for different user data.
impact: Attacker with valid secret reads any user's PII (name, insurance, email, address) — GDPR-relevant. Severity: HIGH.
testability: AUTH_HELPED
[PARKED] Two-tier auth middleware: 55, AUTH_HELPED — needs valid key to confirm whether differential behavior exists; interesting signal but not a standalone finding without live key test
[PARKED] Catalog discrepancy /cat_detail/: 42, AUTH_HELPED — catalog mismatch confirmed but below 45 threshold and impact is speculative without POST schema
[FINAL] 1. Unauthenticated API catalog disclosure (MISCONFIG, 88) — PASSIVE, verified
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid key
[FINAL] 3. BOLA on /settlement_report (BUSLOGIC, 60) — AUTH_HELPED, needs valid scoped key
[NEXT] PROBE: HEAD https://api.kassenkompass.de/ with custom Origin header (e.g. https://evil.com) — confirm CORS policy on root endpoint; also test whether /health/ leaks additional headers (Cache-Control, Server-Timing) that weren't captured. If nothing new, pivot: enumerate kassenkompass.de frontend for OAuth flows, password-reset logic, or admin panels that might leak credentials usable as X-API-Secret.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is authoritative in structure but not in method-spec.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Three distinct auth error paths (RFC 9457 403 message A, RFC 9457 403 message B, HTTP 200 + error body on /sync/) — indicates separate auth middleware stacks, potential scoping differential.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 in RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here.
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed again this session.
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed.
[RISK] kassenkompass: 40/100. Auth genuinely enforced across all data endpoints with three distinct handler paths; no passive bypass found. Unauthenticated catalog disclosure + differential error messages reveal internal architecture but don't directly enable data access. High-value targets (IDOR/BOLA on /user/ and /settlement_report/) gated behind single shared X-API-Secret — AUTH_HELPED only. No source code, Cloudflare-fronted, PHP 8.4.3. Broadening surface: check frontend OAuth/credential flows for potential secret leakage vectors.
## 2026-09-04 09:47:29 UTC [target] (model bigpickle)
[NEW] Two distinct 403 error messages across API endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — two separate auth middleware stacks
[NEW] `/cat_detail/` catalog says GET but returns 405, requires POST — catalog method-spec inaccuracy
[CHANGED] Settlement_report endpoint confirmed: proper 401/403 RFC 9457 format — no misconfiguration here
[CHANGED] `/sync/` remains sole endpoint returning HTTP 200 + auth error body
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=10 tech_exposure=10 cloud_surface=4 gate_ease=8 freshness=8
[PRIO] kassenkompass.de,5.55,attack_surface=5 business_value=8 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[PRIO] www.kassenkompass.de,5.15,attack_surface=5 business_value=6 tech_exposure=3 cloud_surface=2 gate_ease=8 freshness=8
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: Root endpoint `/` and all catch-all paths return full 15-endpoint catalog (including /user/{ext_id}, /delete/{id}, /cancel/{id}, /settlement_report/{year}/{month}) without any authentication; violates least privilege; enables attacker to map attack surface for targeted testing. Already confirmed across multiple sessions.
evidence_needed: Already confirmed; no additional evidence required.
verify_steps: PASSIVE: GET https://api.kassenkompass.de/ — returns full catalog JSON. Already verified.
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw.
testability: PASSIVE
[HYP] IDOR on /user/{ext_id} — cross-user PII access
class: IDOR
asset: api.kassenkompass.de
confidence: 62
reasoning: GET /user/{ext_id} returns "Userdaten abrufen"; ext_id is external/enumerable; single shared X-API-Secret with no visible resource scoping in catalog. The endpoint uses a distinct auth middleware (message B: "Ungültiger X-API-Secret") from most other endpoints (message A: "ungültig oder nicht berechtigt") — if authorization is not per-resource, any valid secret reads any user.
evidence_needed: Valid X-API-Secret; GET /user/1 vs /user/2 produce different PII.
verify_steps: WITH AUTH: GET /user/1, /user/2 with valid secret; compare bodies for different user data.
impact: Attacker with valid secret reads any user's PII (name, insurance, email, address) — GDPR-relevant. Severity: HIGH.
testability: AUTH_HELPED
[HYP] BOLA on /settlement_report/{year}/{month} — cross-tenant financial data
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 60
reasoning: `/settlement_report/{year}/{month}` returns financial settlement reports (CSV/json) via X-API-Secret only; uses error message A ("ungültig oder nicht berechtigt") consistent with group-A endpoints; no evidence report access is scoped to the secret's partner/insurer tenant. If authz only checks header validity, any valid secret retrieves any tenant's report for any year/month.
evidence_needed: Valid X-API-Secret; GET /settlement_report/2025/01 for other tenants differs.
verify_steps: WITH AUTH: GET /settlement_report/2024/01, /settlement_report/2023/12 with valid secret; observe cross-tenant data.
impact: Attacker with valid secret exfiltrates financial/commission settlement data across partners/insurers. Severity: HIGH.
testability: AUTH_HELPED
[PARKED] Two-tier auth middleware differential: confidence 55, AUTH_HELPED — interesting architectural signal (two 403 messages + /sync/ 200 path = three middleware stacks) but not a standalone finding without valid key to confirm scoping differential. Park until key obtained.
[PARKED] Catalog discrepancy /cat_detail/: confidence 42, AUTH_HELPED — below 40 threshold, impact speculative without POST schema. Park.
[FINAL] 1. Unauthenticated API catalog disclosure (MISCONFIG, 90) — PASSIVE, verified across 4+ sessions
[FINAL] 2. IDOR on /user/{ext_id} (IDOR, 62) — AUTH_HELPED, needs valid key; distinct auth middleware makes this more interesting
[FINAL] 3. BOLA on /settlement_report (BUSLOGIC, 60) — AUTH_HELPED, needs valid scoped key
[NEXT] HUMAN: Obtain valid X-API-Secret to unlock AUTH_HELPED hypotheses (IDOR /user/{ext_id}, BOLA /settlement_report, two-tier middleware differential test). All passive avenues exhausted: CORS rejected, CRED_REUSE rejected, frontend OAuth enumeration not yet attempted. Secondary probe if key obtained: test valid secret against /user/1 (middleware B) vs /health_insurance/ (middleware A) to confirm differential authorization scoping.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative.
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ remains sole endpoint returning HTTP 200 + auth error body (known from prior sessions).
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here.
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions.
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed.
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No user-supplied URL/webhook/fetch in catalog; no metadata path.
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Custom X-API-Secret header, not JWT — class not applicable.
[RISK] kassenkompass: 42/100. Auth genuinely enforced across all data endpoints with three distinct handler paths (two RFC 9457 403 messages + /sync/ HTTP 200 path); no passive bypass found. Unauthenticated catalog disclosure + differential error messages reveal internal architecture but don't directly enable data access. High-value IDOR/BOLA gated behind single shared X-API-Secret — AUTH_HELPED only. All passive credential-reuse, CORS, SSRF vectors exhausted. Frontend OAuth enumeration not yet completed but no evidence of OAuth SSO flows found on login pages (PHP form-based auth). Two-tier middleware differential is a structural signal worth testing with a valid key but not a standalone finding. No source code, Cloudflare-fronted, PHP 8.4.3.
## 2026-09-04 14:08:20 UTC [target] (model bigpickle)
