## 2026-09-03 17:32:32 UTC [target] (model nemotron3)
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
## 2026-09-03 20:00:34 UTC [target] (model nemotron3)
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
## 2026-09-03 22:32:11 UTC [target] (model nemotron3)
[NEW] /sync/ returns HTTP 200 with auth error body `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` — status code misconfiguration (should be 401)
[NEW] /health/ unprotected, discloses PHP version via `x-powered-by: PHP/8.4.3`
[NEW] All login forms (`/login_kd.php`, `/login_kk.php`, `/login_partner.php`) and password reset forms lack CSRF tokens
[NEW] Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`
[NEW] `/insurance_info/{kk_id}` returns proper RFC 9457 401 error — inconsistent error handling vs `/sync/`
[NEW] No password reset for insurer portal (`/pw_reset_kk.php` returns 404)
[CHANGED] API catalog confirmed 15 endpoints; `/health/` only fully unprotected endpoint
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: Root endpoint `/` returns full 15-endpoint catalog without auth; violates least privilege; enables attacker to map attack surface (user data, deletion, financial reports) for targeted testing
evidence_needed: Confirm catalog matches actual implemented endpoints; verify no rate-limiting on catalog endpoint
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 15 endpoints respond
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw
testability: PASSIVE
[HYP] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion
class: BUSLOGIC
asset: api.kassenkompass.de
confidence: 70
reasoning: Catalog exposes `/delete/{id}` as "Löschen" (destructive); X-API-Secret auth is single-header; no evidence of resource-level authorization in catalog; if authz checks only validate header presence not resource ownership, any valid secret deletes any ID
evidence_needed: Valid X-API-Secret to test cross-resource deletion; or evidence that secret scope is not resource-bound
verify_steps: GET https://api.kassenkompass.de/delete/1 (no auth → expect 401); with valid secret: GET /delete/1, /delete/2, /delete/999999 — compare responses for authz enforcement
impact: Authenticated user deletes other users'/partners' records (settlements, user data, configs); HIGH
testability: AUTH_HELPED
[HYP] Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 85
reasoning: `/sync/` returns HTTP 200 with `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` while `/insurance_info/{kk_id}` returns proper RFC 9457 401; behavioral misconfiguration could bypass automated scanners expecting 4xx/5xx for auth failures
evidence_needed: Confirm scanner bypass potential; enumerate all endpoints for error handling consistency
verify_steps: GET https://api.kassenkompass.de/sync/ (no auth → 200 with error body); GET https://api.kassenkompass.de/insurance_info/1 (no auth → 401 RFC 9457); test other catalog endpoints for error shape
impact: Auth failures hidden from automated security tooling; delays detection of auth bypass flaws; MEDIUM
testability: PASSIVE
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE) — TOP PRIORITY
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)
[NEXT] PROBE: GET https://api.kassenkompass.delete/1 — confirm auth requirement and error shape for destructive endpoint (read-only, no mutation)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-04 00:35:28 UTC [target] (model nemotron3)
[NEW] `/sync/` with any X-API-Secret value returns distinct error `"Ungültiger X-API-Secret"` (invalid) vs `"fehlt"` (missing) — auth gate genuinely enforced, not bypassable by header presence alone  
[NEW] Partner password-reset magic `KKX3382745` does NOT authenticate as API secret — no cross-asset credential reuse  
[NEW] No `access-control-allow-origin` reflection for arbitrary Origin on api — CORS misconfig REJECTED  
[NEW] `/post/` also requires X-API-Secret; GET/OPTIONS reveal no bypass  
[CHANGED] All API data endpoints remain auth-gated; no egress to AUTH_HELPED hypotheses this session  
[CHANGED] Probe confirmation: `/user/1`, `/delete/1`, `/user/100`, `/insurance_info/1`, `/settlement_report/9999/13` all return HTTP 401 without auth  
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8  
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7  
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6  
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon  
class: MISCONFIG  
asset: api.kassenkompass.de  
confidence: 90  
reasoning: Root endpoint `/` and all catch-all paths return full 15-endpoint catalog (including /user/{ext_id}, /delete/{id}, /cancel/{id}, /settlement_report/{year}/{month}) without any authentication; violates least privilege; enables attacker to map attack surface for targeted testing  
evidence_needed: Confirm catalog matches actual implemented endpoints; verify no rate-limiting on catalog endpoint  
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 15 endpoints respond  
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw  
testability: PASSIVE  
[HYP] Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401  
class: MISCONFIG  
asset: api.kassenkompass.de  
confidence: 85  
reasoning: `/sync/` returns HTTP 200 with `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` while `/insurance_info/{kk_id}` returns proper RFC 9457 401; behavioral misconfiguration could bypass automated scanners expecting 4xx/5xx for auth failures  
evidence_needed: Confirm scanner bypass potential; enumerate all endpoints for error handling consistency  
verify_steps: GET https://api.kassenkompass.de/sync/ (no auth → 200 with error body); GET https://api.kassenkompass.de/insurance_info/1 (no auth → 401 RFC 9457); test other catalog endpoints for error shape  
impact: Auth failures hidden from automated security tooling; delays detection of auth bypass flaws; MEDIUM  
testability: PASSIVE  
[HYP] OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals  
class: OATH  
asset: kassenkompass.de  
confidence: 55  
reasoning: Three distinct login portals (customer/partner/insurer) on same domain; common pattern: shared OAuth/SSO implementation with weak redirect_uri allowlist (subdomain/wildcard) enabling code theft via open redirect or subdomain takeover  
evidence_needed: OAuth authorize endpoint location; redirect_uri parameter handling; allowlist configuration  
verify_steps: GET https://kassenkompass.de/login (identify OAuth flow); GET /authorize?redirect_uri=https://evil.com — check validation; test subdomain wildcard (partner.kassenkompass.de, insurer.kassenkompass.de)  
impact: Account takeover via authorization code theft across all three portal types; CRITICAL  
testability: PASSIVE  
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret  
[PARKED] IDOR on /user/{ext_id} — Cross-User PII Access: confidence 62 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret  
[PARKED] BOLA on /settlement_report/{year}/{month} — Cross-Tenant Financial Data: confidence 60 but AUTH_HELPED — requires valid scoped X-API-Secret; no passive path to obtain secret  
[PARKED] Missing CSRF tokens on login/password-reset forms: confidence 65 but CSRF on anonymous forms is explicitly OUT OF SCOPE per scope.yml  
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE)  
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)  
[FINAL] 3. OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals (confidence 55, PASSIVE)  
[NEXT] PROBE: GET https://kassenkompass.de/login — identify OAuth authorize endpoint location and redirect_uri parameter handling (read-only, passive enumeration)  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners  
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified  
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable  
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins  
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret  
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-04 05:10:05 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: Root endpoint `/` and all catch-all paths return full 15-endpoint catalog (including /user/{ext_id}, /delete/{id}, /cancel/{id}, /settlement_report/{year}/{month}) without any authentication; violates least privilege; enables attacker to map attack surface for targeted testing
evidence_needed: Confirm catalog matches actual implemented endpoints; verify no rate-limiting on catalog endpoint
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 15 endpoints respond
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw
testability: PASSIVE
[HYP] Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 85
reasoning: `/sync/` returns HTTP 200 with `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` while `/insurance_info/{kk_id}` returns proper RFC 9457 401; behavioral misconfiguration could bypass automated scanners expecting 4xx/5xx for auth failures
evidence_needed: Confirm scanner bypass potential; enumerate all endpoints for error handling consistency
verify_steps: GET https://api.kassenkompass.de/sync/ (no auth → 200 with error body); GET https://api.kassenkompass.de/insurance_info/1 (no auth → 401 RFC 9457); test other catalog endpoints for error shape
impact: Auth failures hidden from automated security tooling; delays detection of auth bypass flaws; MEDIUM
testability: PASSIVE
[HYP] OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals
class: OATH
asset: kassenkompass.de
confidence: 55
reasoning: Three distinct login portals (customer/partner/insurer) on same domain; common pattern: shared OAuth/SSO implementation with weak redirect_uri allowlist (subdomain/wildcard) enabling code theft via open redirect or subdomain takeover
evidence_needed: OAuth authorize endpoint location; redirect_uri parameter handling; allowlist configuration
verify_steps: GET https://kassenkompass.de/login (identify OAuth flow); GET /authorize?redirect_uri=https://evil.com — check validation; test subdomain wildcard (partner.kassenkompass.de, insurer.kassenkompass.de)
impact: Account takeover via authorization code theft across all three portal types; CRITICAL
testability: PASSIVE
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] IDOR on /user/{ext_id} — Cross-User PII Access: confidence 62 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /settlement_report/{year}/{month} — Cross-Tenant Financial Data: confidence 60 but AUTH_HELPED — requires valid scoped X-API-Secret; no passive path to obtain secret
[PARKED] Missing CSRF tokens on login/password-reset forms: confidence 65 but CSRF on anonymous forms is explicitly OUT OF SCOPE per scope.yml
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE)
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)
[FINAL] 3. OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals (confidence 55, PASSIVE)
[NEXT] PROBE: GET https://kassenkompass.de/login — identify OAuth authorize endpoint location and redirect_uri parameter handling (read-only, passive enumeration)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-04 09:51:30 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: Root endpoint `/` and all catch-all paths return full 15-endpoint catalog (including `/user/{ext_id}`, `/delete/{id}`, `/cancel/{id}`, `/settlement_report/{year}/{month}`) without any authentication; violates least privilege; enables attacker to map attack surface for targeted testing
evidence_needed: Confirm catalog matches actual implemented endpoints; verify no rate-limiting on catalog endpoint
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 15 endpoints respond
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw
testability: PASSIVE
[HYP] Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 85
reasoning: `/sync/` returns HTTP 200 with `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` while `/insurance_info/{kk_id}`, `/user/{ext_id}`, `/settlement_report/{year}/{month}` return proper RFC 9457 401; behavioral misconfiguration could bypass automated scanners expecting 4xx/5xx for auth failures
evidence_needed: Confirm scanner bypass potential; enumerate all endpoints for error handling consistency
verify_steps: GET https://api.kassenkompass.de/sync/ (no auth → 200 with error body); GET https://api.kassenkompass.de/insurance_info/1 (no auth → 401 RFC 9457); test other catalog endpoints for error shape
impact: Auth failures hidden from automated security tooling; delays detection of auth bypass flaws; MEDIUM
testability: PASSIVE
[HYP] Two-Tier Auth Middleware — Differential 403 Messages Suggest Scoping Bypass Potential
class: AUTH
asset: api.kassenkompass.de
confidence: 60
reasoning: Two distinct 403 error messages observed across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — suggests two separate auth middleware paths with potentially different scoping logic; could allow cross-tenant access if middleware misapplied
evidence_needed: Map which endpoints use which error message; test with valid-but-wrong-scope secret on `/user/{ext_id}` vs others
verify_steps: GET https://api.kassenkompass.de/user/1 with invalid X-API-Secret (expect 403 "Ungültiger X-API-Secret"); GET https://api.kassenkompass.de/insurance_info/1 with invalid X-API-Secret (expect 403 "ungültig oder nicht berechtigt"); compare response bodies
impact: If middleware scoping differs, valid secret for one endpoint class may grant access to another; potential BOLA across tenant boundaries; HIGH
testability: AUTH_HELPED
[PARKED] OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals: No OAuth authorize endpoint discovered in passive enumeration; all three portals use traditional form-post auth; hypothesis not verifiable passively
[PARKED] IDOR on /user/{ext_id} — Cross-User PII Access: AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /settlement_report/{year}/{month} — Cross-Tenant Financial Data: AUTH_HELPED — requires valid scoped X-API-Secret; no passive path to obtain secret
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE)
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)
[FINAL] 3. Two-Tier Auth Middleware — Differential 403 Messages Suggest Scoping Bypass Potential (confidence 60, AUTH_HELPED)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message variant "Ungültiger X-API-Secret" vs other endpoints' "ungültig oder nicht berechtigt" (read-only, passive enumeration of error shape)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is authoritative in structure but not in method-spec
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Three distinct auth error paths (RFC 9457 403 message A, RFC 9457 403 message B, HTTP 200 + error body on /sync/) — indicates separate auth middleware stacks, potential scoping differential
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-04 14:20:58 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 90
reasoning: Root endpoint `/` and all catch-all paths return full 15-endpoint catalog (including `/user/{ext_id}`, `/delete/{id}`, `/cancel/{id}`, `/settlement_report/{year}/{month}`) without any authentication; violates least privilege; enables attacker to map attack surface for targeted testing
evidence_needed: Confirm catalog matches actual implemented endpoints; verify no rate-limiting on catalog endpoint
verify_steps: GET https://api.kassenkompass.de/ (already done); GET https://api.kassenkompass.de/user/1 (401); GET https://api.kassenkompass.de/delete/1 (401); confirm all 15 endpoints respond
impact: Attacker gains full API map for targeted auth-bypass, IDOR, BOLA testing; reduces reconnaissance from hours to seconds; HIGH if any endpoint has auth flaw
testability: PASSIVE
[HYP] Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401
class: MISCONFIG
asset: api.kassenkompass.de
confidence: 85
reasoning: `/sync/` returns HTTP 200 with `{"table":401,"success":false,"message":"X-API-Secret Header fehlt"}` while `/insurance_info/{kk_id}`, `/user/{ext_id}`, `/settlement_report/{year}/{month}` return proper RFC 9457 401; behavioral misconfiguration could bypass automated scanners expecting 4xx/5xx for auth failures
evidence_needed: Confirm scanner bypass potential; enumerate all endpoints for error handling consistency
verify_steps: GET https://api.kassenkompass.de/sync/ (no auth → 200 with error body); GET https://api.kassenkompass.de/insurance_info/1 (no auth → 401 RFC 9457); test other catalog endpoints for error shape
impact: Auth failures hidden from automated security tooling; delays detection of auth bypass flaws; MEDIUM
testability: PASSIVE
[HYP] Two-Tier Auth Middleware — Differential 403 Messages Suggest Scoping Bypass Potential
class: AUTH
asset: api.kassenkompass.de
confidence: 60
reasoning: Two distinct 403 error messages observed across endpoints — "ungültig oder nicht berechtigt" (8 endpoints: /settlement_report/, /question_tree/, /health_insurance/, /health_insurance_savings/, /health_insurance_comparison/, /detail_comparison/, /state/, /insurance_info/{kk_id}) vs "Ungültiger X-API-Secret" (only `/user/{ext_id}`) — suggests two separate auth middleware paths with potentially different scoping logic; could allow cross-tenant access if middleware misapplied
evidence_needed: Map which endpoints use which error message; test with valid-but-wrong-scope secret on `/user/{ext_id}` vs others
verify_steps: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` (expect 403 "Ungültiger X-API-Secret"); GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` (expect 403 "ungültig oder nicht berechtigt"); compare response bodies
impact: If middleware scoping differs, valid secret for one endpoint class may grant access to another; potential BOLA across tenant boundaries; HIGH
testability: AUTH_HELPED
[PARKED] Two-Tier Auth Middleware — Differential 403 Messages Suggest Scoping Bypass Potential: confidence 60 but AUTH_HELPED — requires valid X-API-Secret to test differential authorization scoping; no passive path to obtain secret; architectural signal only without live key
[PARKED] IDOR on /user/{ext_id} — Cross-User PII Access: confidence 62 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /settlement_report/{year}/{month} — Cross-Tenant Financial Data: confidence 60 but AUTH_HELPED — requires valid scoped X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; destructive endpoint; no safe passive verification
[PARKED] OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals: confidence 55 but no OAuth authorize endpoint discovered in passive enumeration; all three portals use traditional form-post auth; hypothesis not verifiable passively
[PARKED] Missing CSRF tokens on login/password-reset forms: confidence 65 but CSRF on anonymous forms is explicitly OUT OF SCOPE per scope.yml
[PARKED] /cat_detail/ Catalog Method Mismatch: confidence 42 but AUTH_HELPED — catalog discrepancy confirmed (GET vs POST) but impact speculative without POST schema; below 45 threshold
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE)
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message variant "Ungültiger X-API-Secret" vs other endpoints' "ungültig oder nicht berechtigt" (read-only, passive enumeration of error shape)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
