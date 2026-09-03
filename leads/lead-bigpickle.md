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
