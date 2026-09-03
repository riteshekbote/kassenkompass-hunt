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
