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
## 2026-09-04 17:42:44 UTC [target] (model nemotron3)
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
[HYP] Weak Static Magic Values in Partner/Customer Password Reset Flows
class: AUTH
asset: kassenkompass.de
confidence: 55
reasoning: Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`; both are short, predictable values that could be brute-forced or discovered via source code exposure; no rate limiting observed on reset endpoints in prior reconnaissance
evidence_needed: Confirm magic value is static per partner/customer or global; test rate limiting on reset endpoints; check if magic value appears in client-side code or logs
verify_steps: GET https://kassenkompass.de/pw_reset_partner.php (observe form structure); POST to reset endpoint with magic value variations; test brute-force protection via repeated submissions
impact: Partner/customer account takeover via password reset; access to portals with PII and insurance comparison data
testability: PASSIVE
[HYP] Subdomain Mirror Configuration Drift — www.kassenkompass.de Divergence
class: MISCONFIG
asset: www.kassenkompass.de
confidence: 45
reasoning: Inventory marks www.kassenkompass.de as mirror of kassenkompass.de; mirrors often drift in headers, CSP, cookie scopes, or exposed debug endpoints; no independent verification of parity in current dataset
evidence_needed: Compare security headers, CSP, cookie attributes, and endpoint exposure between www and apex domain
verify_steps: GET https://www.kassenkompass.de/ (compare headers/body vs kassenkompass.de); GET https://www.kassenkompass.de/login_kd.php (check form parity); OPTIONS on both for CORS differences
impact: Weaker security posture on www subdomain could bypass controls on primary domain; cookie scope misconfiguration could leak sessions across subdomains
testability: PASSIVE
[PARKED] Two-Tier Auth Middleware — Differential 403 Messages Suggest Scoping Bypass Potential: confidence 60 but AUTH_HELPED — requires valid X-API-Secret to test differential authorization scoping; no passive path to obtain secret
[PARKED] IDOR on /user/{ext_id} — Cross-User PII Access: confidence 62 but AUTH_HELPED — requires valid X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /settlement_report/{year}/{month} — Cross-Tenant Financial Data: confidence 60 but AUTH_HELPED — requires valid scoped X-API-Secret; no passive path to obtain secret
[PARKED] BOLA on /delete/{id} — Authenticated Arbitrary Resource Deletion: confidence 70 but AUTH_HELPED — requires valid X-API-Secret; destructive endpoint; no safe passive verification
[PARKED] OAuth redirect_uri Validation Bypass Across Multi-Tenant Login Portals: confidence 55 but no OAuth authorize endpoint discovered in passive enumeration; all three portals use traditional form-post auth; hypothesis not verifiable passively
[PARKED] Missing CSRF tokens on login/password-reset forms: confidence 65 but CSRF on anonymous forms is explicitly OUT OF SCOPE per scope.yml
[PARKED] /cat_detail/ Catalog Method Mismatch: confidence 42 but AUTH_HELPED — catalog discrepancy confirmed (GET vs POST) but impact speculative without POST schema; below 45 threshold
[FINAL] 1. API Endpoint Catalog Disclosure Enables Targeted IDOR/BOLA Recon (confidence 90, PASSIVE)
[FINAL] 2. Inconsistent Auth Error Handling — /sync/ Returns 200 Instead of 401 (confidence 85, PASSIVE)
[FINAL] 3. Weak Static Magic Values in Partner/Customer Password Reset Flows (confidence 55, PASSIVE)
[FINAL] 4. Subdomain Mirror Configuration Drift — www.kassenkompass.de Divergence (confidence 45, PASSIVE)
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
## 2026-09-04 20:04:15 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion
class: AUTH
asset: api.kassenkompass.de
confidence: 65
reasoning: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints: /settlement_report/, /question_tree/, /health_insurance/, /health_insurance_savings/, /health_insurance_comparison/, /detail_comparison/, /state/, /insurance_info/{kk_id}) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — confirms two separate auth middleware paths; /sync/ adds third error path (HTTP 200 + body); middleware separation suggests different authorization scoping logic that could be confused
evidence_needed: Map all 15 endpoints to their respective 403 error message variant; confirm middleware assignment is endpoint-based not secret-scope-based
verify_steps: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` (expect 403 "Ungültiger X-API-Secret"); GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` (expect 403 "ungültig oder nicht berechtigt"); GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` (expect 403 variant); repeat for all catalog endpoints
impact: If middleware scoping differs, valid secret issued for one endpoint class (e.g., comparison endpoints) may be accepted by another middleware (e.g., /user/{ext_id}) enabling cross-tenant PII access; HIGH
testability: PASSIVE
[HYP] Weak Static Magic Values in Partner/Customer Password Reset Flows
class: AUTH
asset: kassenkompass.de
confidence: 55
reasoning: Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`; both are short, predictable, global constants; no rate limiting observed on reset endpoints in prior reconnaissance; magic values not tied to user session or time-limited tokens
evidence_needed: Confirm magic value is global (not per-partner/customer); verify no rate limiting or CAPTCHA on reset submission; check if magic value appears in client-side JS or leaked in logs
verify_steps: GET https://kassenkompass.de/pw_reset_partner.php (observe form structure, hidden fields); POST to partner reset endpoint with magic `KKX3382745` and arbitrary email; repeat 10x rapidly to test rate limiting; GET https://kassenkompass.de/login_kd.php (customer login form) inspect for `X8372` usage
impact: Partner/customer account takeover via password reset; access to portals with PII, health data, insurance comparisons; HIGH
testability: PASSIVE
[HYP] Subdomain Mirror Configuration Drift — www.kassenkompass.de Security Header Divergence
class: MISCONFIG
asset: www.kassenkompass.de
confidence: 48
reasoning: Inventory marks www.kassenkompass.de as mirror of kassenkompass.de; mirrors commonly drift in CSP, HSTS, cookie flags (SameSite, Secure, Domain), exposed debug endpoints, or header disclosure (Server, X-Powered-By); no independent header/body comparison performed in current dataset
evidence_needed: Full security header diff between www and apex; cookie scope/attribute comparison; endpoint enumeration parity check
verify_steps: GET https://www.kassenkompass.de/ (capture all response headers, body hash); GET https://kassenkompass.de/ (capture all response headers, body hash); diff headers (CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Set-Cookie attributes); GET https://www.kassenkompass.de/login_kd.php vs https://kassenkompass.de/login_kd.php (form parity); OPTIONS both for CORS header differences
impact: Weaker security posture on www could bypass controls on primary domain; cookie Domain misconfiguration could leak sessions across subdomains; missing CSP/HSTS on www enables MITM/XSS chains; MEDIUM
testability: PASSIVE
[PARKED] Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion: confidence 65 but AUTH_HELPED for full exploitation (requires valid secret to test cross-middleware acceptance); passive mapping of error variants only confirms architectural separation, not exploitability
[PARKED] Weak Static Magic Values in Partner/Customer Password Reset Flows: confidence 55 but brute-force/rate-limit testing edges toward active auth interaction; program scope allows passive enumeration only for auth flows
[PARKED] Subdomain Mirror Configuration Drift: confidence 48 near threshold; impact speculative without confirmed divergence
[FINAL] 1. Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion (confidence 65, PASSIVE mapping only)
[FINAL] 2. Weak Static Magic Values in Partner/Customer Password Reset Flows (confidence 55, PASSIVE)
[FINAL] 3. Subdomain Mirror Configuration Drift — www.kassenkompass.de Security Header Divergence (confidence 48, PASSIVE)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` — confirm 403 error message "ungültig oder nicht berechtigt"; GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` — map third endpoint to middleware variant (read-only, passive error-shape enumeration, 1 rps)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; two-tier auth middleware suggests scoping complexity; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-04 22:18:20 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[HYP] Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion
class: AUTH
asset: api.kassenkompass.de
confidence: 65
reasoning: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints: /settlement_report/, /question_tree/, /health_insurance/, /health_insurance_savings/, /health_insurance_comparison/, /detail_comparison/, /state/, /insurance_info/{kk_id}) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — confirms two separate auth middleware paths; /sync/ adds third error path (HTTP 200 + body); middleware separation suggests different authorization scoping logic that could be confused
evidence_needed: Map all 15 endpoints to their respective 403 error message variant; confirm middleware assignment is endpoint-based not secret-scope-based
verify_steps: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` (expect 403 "Ungültiger X-API-Secret"); GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` (expect 403 "ungültig oder nicht berechtigt"); GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` (expect 403 variant); repeat for all catalog endpoints
impact: If middleware scoping differs, valid secret issued for one endpoint class (e.g., comparison endpoints) may be accepted by another middleware (e.g., /user/{ext_id}) enabling cross-tenant PII access; HIGH
testability: PASSIVE
[HYP] Weak Static Magic Values in Partner/Customer Password Reset Flows
class: AUTH
asset: kassenkompass.de
confidence: 55
reasoning: Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`; both are short, predictable, global constants; no rate limiting observed on reset endpoints in prior reconnaissance; magic values not tied to user session or time-limited tokens
evidence_needed: Confirm magic value is global (not per-partner/customer); verify no rate limiting or CAPTCHA on reset submission; check if magic value appears in client-side JS or leaked in logs
verify_steps: GET https://kassenkompass.de/pw_reset_partner.php (observe form structure, hidden fields); POST to partner reset endpoint with magic `KKX3382745` and arbitrary email; repeat 10x rapidly to test rate limiting; GET https://kassenkompass.de/login_kd.php (customer login form) inspect for `X8372` usage
impact: Partner/customer account takeover via password reset; access to portals with PII, health data, insurance comparisons; HIGH
testability: PASSIVE
[HYP] Subdomain Mirror Configuration Drift — www.kassenkompass.de Security Header Divergence
class: MISCONFIG
asset: www.kassenkompass.de
confidence: 48
reasoning: Inventory marks www.kassenkompass.de as mirror of kassenkompass.de; mirrors commonly drift in CSP, HSTS, cookie flags (SameSite, Secure, Domain), exposed debug endpoints, or header disclosure (Server, X-Powered-By); no independent header/body comparison performed in current dataset
evidence_needed: Full security header diff between www and apex; cookie scope/attribute comparison; endpoint enumeration parity check
verify_steps: GET https://www.kassenkompass.de/ (capture all response headers, body hash); GET https://kassenkompass.de/ (capture all response headers, body hash); diff headers (CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Set-Cookie attributes); GET https://www.kassenkompass.de/login_kd.php vs https://kassenkompass.de/login_kd.php (form parity); OPTIONS both for CORS header differences
impact: Weaker security posture on www could bypass controls on primary domain; cookie Domain misconfiguration could leak sessions across subdomains; missing CSP/HSTS on www enables MITM/XSS chains; MEDIUM
testability: PASSIVE
[PARKED] Subdomain Mirror Configuration Drift — www.kassenkompass.de Security Header Divergence: confidence 48 near threshold; impact speculative without confirmed divergence
[FINAL] 1. Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion (confidence 65, PASSIVE mapping only)
[FINAL] 2. Weak Static Magic Values in Partner/Customer Password Reset Flows (confidence 55, PASSIVE)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` — confirm 403 error message "ungültig oder nicht berechtigt"; GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` — map third endpoint to middleware variant (read-only, passive error-shape enumeration, 1 rps)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; two-tier auth middleware suggests scoping complexity; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-05 00:18:34 UTC [target] (model nemotron3)
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,6.7,attack_surface=7 business_value=8 tech_exposure=6 gate_ease=5 cloud_surface=6 freshness=7
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
class: BUSLOGIC  
asset: api.kassenkompass.de  
confidence: 58  
reasoning: `/v2/insurance_info/{kk_id}` (v2.0 "breite Variante") returns draft categories + resolved references — undocumented in 4+ prior recon sessions; widest per-request data surface on API. v2 router uses greedy segment match (`/v2/insurance_info/{anything}` all reach protected handler 401), kk_id not validated at routing. If a valid X-API-Secret scoped for v1 comparison endpoints is accepted by v2 middleware, cross-version authorization bypass exposes draft/unreleased insurance data across all insurers.  
evidence_needed: Valid X-API-Secret tested against v2 endpoint; confirm response contains draft categories not in v1 `/insurance_info/{kk_id}`; verify v2 middleware accepts v1-issued secrets.  
verify_steps: GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: invalid` — confirm 401/403 error shape (passive); GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: KKX3382745` — rule out cross-asset credential reuse (passive); WITH AUTH: GET /v2/insurance_info/1 vs /insurance_info/1 with valid secret — compare data breadth (AUTH_HELPED).  
impact: Cross-version BOLA exposing draft insurance categories + resolved references across all insurers; GDPR-relevant if draft includes PII; HIGH.  
testability: PASSIVE (error-shape enumeration), AUTH_HELPED (data differential)
class: AUTH  
asset: api.kassenkompass.de  
confidence: 65  
reasoning: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints: /settlement_report/, /question_tree/, /health_insurance/, /health_insurance_savings/, /health_insurance_comparison/, /detail_comparison/, /state/, /insurance_info/{kk_id}) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — confirms two separate auth middleware paths; /sync/ adds third error path (HTTP 200 + body). Middleware separation suggests different authorization scoping logic that could be confused.  
evidence_needed: Map all 15 endpoints to their respective 403 error message variant; confirm middleware assignment is endpoint-based not secret-scope-based.  
verify_steps: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — expect 403 "Ungültiger X-API-Secret"; GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` — expect 403 "ungültig oder nicht berechtigt"; GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` — map third endpoint; repeat for all catalog endpoints (read-only, passive error-shape enumeration, 1 rps).  
impact: If middleware scoping differs, valid secret issued for one endpoint class (e.g., comparison endpoints) may be accepted by another middleware (e.g., /user/{ext_id}) enabling cross-tenant PII access; HIGH.  
testability: PASSIVE
class: AUTH  
asset: kassenkompass.de  
confidence: 55  
reasoning: Partner password reset (`/pw_reset_partner.php`) uses hardcoded magic value `KKX3382745`; customer login uses `X8372`; both are short, predictable, global constants; no rate limiting observed on reset endpoints in prior reconnaissance; magic values not tied to user session or time-limited tokens.  
evidence_needed: Confirm magic value is global (not per-partner/customer); verify no rate limiting or CAPTCHA on reset submission; check if magic value appears in client-side JS or leaked in logs.  
verify_steps: GET https://kassenkompass.de/pw_reset_partner.php (observe form structure, hidden fields); POST to partner reset endpoint with magic `KKX3382745` and arbitrary email; repeat 10x rapidly to test rate limiting; GET https://kassenkompass.de/login_kd.php (customer login form) inspect for `X8372` usage (passive-first, 1 rps).  
impact: Partner/customer account takeover via password reset; access to portals with PII, health data, insurance comparisons; HIGH.  
testability: PASSIVE
[PARKED] Draft-Category BOLA via v2 insurance_info Wide Variant: confidence 58 but requires valid X-API-Secret to confirm cross-version acceptance and data differential; passive-only confirms v2 exists and is protected, not that BOLA is exploitable.
[PARKED] Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion: confidence 65 but full exploitation (cross-middleware secret acceptance) requires valid X-API-Secret; passive mapping of error variants only confirms architectural separation.
[PARKED] Weak Static Magic Values in Partner/Customer Password Reset Flows: confidence 55 but brute-force/rate-limit testing edges toward active auth interaction; program scope allows passive enumeration only for auth flows.
[FINAL] 1. Two-Tier Auth Middleware — Differential 403 Messages Enable Scope Confusion (confidence 65, PASSIVE mapping only)  
[FINAL] 2. Weak Static Magic Values in Partner/Customer Password Reset Flows (confidence 55, PASSIVE)  
[FINAL] 3. Draft-Category BOLA via v2 insurance_info Wide Variant — Unreleased Data Across All Insurers (confidence 58, PASSIVE mapping + AUTH_HELPED for data diff)
[NEXT] PROBE: GET https://api.kassenkompass.de/user/1 with header `X-API-Secret: invalid` — confirm 403 error message "Ungültiger X-API-Secret"; GET https://api.kassenkompass.de/insurance_info/1 with header `X-API-Secret: invalid` — confirm 403 error message "ungültig oder nicht berechtigt"; GET https://api.kassenkompass.de/settlement_report/2024/01 with header `X-API-Secret: invalid` — map third endpoint to middleware variant; GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: invalid` — confirm v2 error shape (read-only, passive error-shape enumeration, 1 rps)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categories + resolved references — undocumented in 4+ prior recon sessions; widest per-request data surface on the API  
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catch-all — versioned endpoint enumeration primitive; only `insurance_info` registered so far  
[LEARN] ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the protected handler (401); kk_id not validated at routing  
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified  
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable  
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions  
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed  
[LEARN] REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed; drift hypothesis dropped  
[RISK] kassenkompass: 72 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; two-tier auth middleware suggests scoping complexity; v2 router exposes unreleased draft data surface; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-05 04:44:08 UTC [target] (model nemotron3)
[NEW] api.kassenkompass.de: v2 router sweep complete — only `insurance_info` registered (24 names tested → router-404 oracle); single-endpoint versioned surface confirmed
[NEW] api.kassenkompass.de: Auth middleware map finalized — v1 majority + v2 share middleware A (`Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`); only `/user/{ext_id}` uses middleware B (`Ungültiger X-API-Secret` + instance echo); `/sync/` legacy HTTP-200 custom JSON — two stacks + one legacy, not three
[NEW] api.kassenkompass.de: X-API-Secret confirmed SOLE auth channel — `Authorization: Bearer`, `X-API-Key`, `X-Api-Token`, `api_key=` query all return 401 "erforderlich" on middleware A and B; no alternate header-name bypass
[NEW] api.kassenkompass.de: Magic `KKX3382745` (sha256 bc2cb4e9…) and `X8372` (sha256 a4197524…) rejected (403) on ALL three auth paths including middleware-B and v2 — CRED_REUSE closed completely
[NEW] kassenkompass.de: Funnel (`bonusrechner.php`) server-side mirrors raw pass-params into 1-year cookies with NO validation — alias map `jid|customerid→customerid`, `agn|connectionnumber→agenturnummer`, `ppn|poolpartnernummer→poolpartnernummer`, plus `employeenumber`, `advisorid`, `frab`
[NEW] kassenkompass.de: Two new dedicated hosts discovered via JS — `awv.kassenkompass.de` (self-hosted GTM proxy, nginx, `/gtm.js?id=GTM-TT4LBVMW`, root=400 noindex) + `load.awv.kassenkompass.de` (Cloudflare-challenged loader) — supersedes prior "0 dedicated hosts" wildcard-DNS finding
[NEW] kassenkompass.de: Funnel entry map from `param_passthrough.js` v=web1.0.0 (commented "kk-web-draft" refactor 2026-08-30) — only `bonusrechner*.php` + `termin.php` are app entry points; server-side cookie injection confirmed
[CHANGED] www.kassenkompass.de: Mirror header drift hypothesis dropped — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,7.2,attack_surface=8 business_value=8 tech_exposure=7 gate_ease=6 cloud_surface=6 freshness=8
[PRIO] awv.kassenkompass.de,5.8,attack_surface=6 business_value=5 tech_exposure=6 gate_ease=5 cloud_surface=5 freshness=9
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[PRIO] load.awv.kassenkompass.de,4.5,attack_surface=4 business_value=4 tech_exposure=5 gate_ease=3 cloud_surface=6 freshness=9
[HYP] Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets
class: AUTH
asset: api.kassenkompass.de
confidence: 62
reasoning: v2 router (`/v2/insurance_info/{kk_id}`) shares middleware A with v1 majority endpoints (identical 403 error wording: `Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`). v2 returns draft categories + resolved references — widest per-request data surface, undocumented in 4+ prior recon sessions. v2 router uses greedy segment match (`/v2/insurance_info/{anything}` all reach protected handler 401), kk_id not validated at routing. If a valid X-API-Secret scoped for v1 comparison endpoints is accepted by v2 middleware, cross-version authorization bypass exposes draft/unreleased insurance data across all insurers.
evidence_needed: Valid X-API-Secret tested against v2 endpoint; confirm response contains draft categories not in v1 `/insurance_info/{kk_id}`; verify v2 middleware accepts v1-issued secrets.
verify_steps: GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: invalid` — confirm 401/403 error shape matches middleware A (passive); GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: KKX3382745` — rule out cross-asset credential reuse (passive); WITH AUTH: GET /v2/insurance_info/1 vs /insurance_info/1 with valid secret — compare data breadth (AUTH_HELPED).
impact: Cross-version BOLA exposing draft insurance categories + resolved references across all insurers; GDPR-relevant if draft includes PII; HIGH.
testability: PASSIVE (error-shape enumeration), AUTH_HELPED (data differential)
[HYP] Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year
class: BUSLOGIC
asset: kassenkompass.de
confidence: 70
reasoning: `bonusrechner.php` server-side mirrors raw pass-params (`lizenz`, `jid`, `agn`, `connectionnumber`, `ppn`, `poolpartnernummer`, `employeenumber`, `advisorid`, `frab`) into 1-year cookies with NO validation. Alias map confirms multiple input names map to same cookie (`jid|customerid→customerid`, `agn|connectionnumber→agenturnummer`, `ppn|poolpartnernummer→poolpartnernummer`). No CSRF tokens on any forms. Cookies set via `Set-Cookie` with `Max-Age=31536000`; no `Secure`/`HttpOnly`/`SameSite` attributes observed in prior recon. Attacker can craft links that poison victim's funnel cookies, potentially hijacking partner/customer session context or injecting fake advisor/poolpartner identity into downstream comparison/quote flows.
evidence_needed: Confirm cookie attributes (Secure/HttpOnly/SameSite) on Set-Cookie headers; verify downstream endpoints trust cookie values without re-validation; test parameter collision (e.g., `jid=X&customerid=Y` — which wins?).
verify_steps: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET); GET https://kassenkompass.de/bonusrechner.php?jid=X&customerid=Y — observe which cookie value wins (passive); GET https://kassenkompass.de/termin.php with poisoned cookies — observe if identity carries into booking flow (passive, requires cookie jar).
impact: Session fixation / identity injection into insurance comparison funnel; partner/advisor impersonation; downstream quote manipulation; MEDIUM-HIGH.
testability: PASSIVE
[HYP] GTM Proxy Subdomain — Self-Hosted Tag Manager with No Index / Potential Config Exposure
class: MISCONFIG
asset: awv.kassenkompass.de
confidence: 55
reasoning: Newly discovered dedicated host `awv.kassenkompass.de` runs self-hosted GTM proxy (nginx) serving `/gtm.js?id=GTM-TT4LBVMW`; root returns 400 noindex. Self-hosted GTM proxies often expose debug endpoints (`/gtm/debug`, `/gtm/preview`, `/gtm/auth`), container config via `/gtm.js?id=GTM-XXXXXX&l=dataLayer`, or misconfigured CORS. `load.awv.kassenkompass.de` is Cloudflare-challenged loader — potential bypass via direct GTM proxy. No prior recon sessions observed these hosts (wildcard DNS previously returned "0 dedicated hosts").
evidence_needed: Enumerate GTM proxy paths (`/gtm/debug`, `/gtm/preview`, `/gtm/auth`, `/gtm.js` with various params); check for container config leakage; test CORS on GTM endpoints; verify if `load.awv.kassenkompass.de` serves distinct content vs proxy.
verify_steps: GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW — confirm GTM proxy behavior (passive); GET https://awv.kassenkompass.de/gtm/debug — probe debug endpoint (passive); GET https://awv.kassenkompass.de/gtm/preview — probe preview endpoint (passive); GET https://awv.kassenkompass.de/ — confirm 400 noindex (passive); GET https://load.awv.kassenkompass.de/ — observe Cloudflare challenge vs content (passive).
impact: GTM container config leakage (marketing tags, custom HTML/JS, dataLayer structure); potential XSS via malicious tag injection if container compromised; reconnaissance amplifier for funnel architecture; LOW-MEDIUM.
testability: PASSIVE
[PARKED] Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets: confidence 62 but requires valid X-API-Secret to confirm cross-version acceptance and data differential; passive-only confirms v2 exists and shares middleware A wording, not that BOLA is exploitable.
[PARKED] Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year: confidence 70 but cookie attribute verification and downstream trust validation requires observing Set-Cookie headers and potentially following redirect chains; passive GET with params is safe but limited.
[FINAL] 1. GTM Proxy Subdomain — Self-Hosted Tag Manager with No Index / Potential Config Exposure (confidence 55, PASSIVE)
[FINAL] 2. Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year (confidence 70, PASSIVE)
[FINAL] 3. Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (confidence 62, PASSIVE mapping + AUTH_HELPED for data diff)
[NEXT] PROBE: GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW — confirm GTM proxy behavior and capture response headers/body; GET https://awv.kassenkompass.de/gtm/debug — probe debug endpoint; GET https://awv.kassenkompass.de/gtm/preview — probe preview endpoint (read-only, passive, 1 rps)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categories + resolved references — undocumented in 4+ prior recon sessions; widest per-request data surface on the API
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catch-all — versioned endpoint enumeration primitive; only `insurance_info` registered so far
[LEARN] ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the protected handler (401); kk_id not validated at routing
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
[LEARN] REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed; drift hypothesis dropped
[LEARN] ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenumber, advisorid, frab) with no validation — alias map jid|customerid→customerid, agn|connectionnumber→agenturnummer, ppn|poolpartnernummer→poolpartnernummer
[LEARN] ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=400 noindex) + load.awv.kassenkompass.de (Cloudflare-challenged) — JS-discovered, supersedes wildcard-DNS "0 dedicated hosts"
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned surface
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt"); only /user/{ext_id} middleware B ("Ungültiger X-API-Secret" + instance echo); /sync/ legacy HTTP-200 custom JSON; two stacks + one legacy, not three
[LEARN] REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X-API-Secret sole channel; no header-name bypass
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
[RISK] kassenkompass: 74 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; two-tier auth middleware suggests scoping complexity; v2 router exposes unreleased draft data surface; funnel cookie injection with 1-year persistence and no validation; new GTM proxy subdomain expands attack surface; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
## 2026-09-05 08:46:00 UTC [target] (model nemotron3)
[NEW] awv.kassenkompass.de: GTM proxy probes completed — `/gtm.js?id=GTM-TT4LBVMW` returns 200 (nginx GTM proxy confirmed); `/gtm/debug` → 404; `/gtm/preview` → 404; root `/` → 404 (not 400); `load.awv.kassenkompass.de/` → 403 (Cloudflare challenge)
[NEW] awv.kassenkompass.de: No debug/preview/auth endpoints exposed on self-hosted GTM proxy — reduces config leakage surface
[CHANGED] awv.kassenkompass.de: Root returns 404 not 400 noindex — prior "400 noindex" was inference; actual response is 404
[PRIO] api.kassenkompass.de,8.6,attack_surface=9 business_value=9 tech_exposure=8 gate_ease=9 cloud_surface=7 freshness=8
[PRIO] kassenkompass.de,7.2,attack_surface=8 business_value=8 tech_exposure=7 gate_ease=6 cloud_surface=6 freshness=8
[PRIO] awv.kassenkompass.de,5.3,attack_surface=5 business_value=5 tech_exposure=5 gate_ease=5 cloud_surface=5 freshness=9
[PRIO] www.kassenkompass.de,5.2,attack_surface=5 business_value=6 tech_exposure=5 gate_ease=4 cloud_surface=5 freshness=6
[PRIO] load.awv.kassenkompass.de,4.5,attack_surface=4 business_value=4 tech_exposure=5 gate_ease=3 cloud_surface=6 freshness=9
[HYP] Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets
class: AUTH
asset: api.kassenkompass.de
confidence: 62
reasoning: v2 router (`/v2/insurance_info/{kk_id}`) shares middleware A with v1 majority endpoints (identical 403 error wording: `Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt`). v2 returns draft categories + resolved references — widest per-request data surface, undocumented in 4+ prior recon sessions. v2 router uses greedy segment match (`/v2/insurance_info/{anything}` all reach protected handler 401), kk_id not validated at routing. If a valid X-API-Secret scoped for v1 comparison endpoints is accepted by v2 middleware, cross-version authorization bypass exposes draft/unreleased insurance data across all insurers.
evidence_needed: Valid X-API-Secret tested against v2 endpoint; confirm response contains draft categories not in v1 `/insurance_info/{kk_id}`; verify v2 middleware accepts v1-issued secrets.
verify_steps: GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: invalid` — confirm 401/403 error shape matches middleware A (passive); GET https://api.kassenkompass.de/v2/insurance_info/1 with header `X-API-Secret: KKX3382745` — rule out cross-asset credential reuse (passive); WITH AUTH: GET /v2/insurance_info/1 vs /insurance_info/1 with valid secret — compare data breadth (AUTH_HELPED).
impact: Cross-version BOLA exposing draft insurance categories + resolved references across all insurers; GDPR-relevant if draft includes PII; HIGH.
testability: PASSIVE (error-shape enumeration), AUTH_HELPED (data differential)
[HYP] Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year
class: BUSLOGIC
asset: kassenkompass.de
confidence: 70
reasoning: `bonusrechner.php` server-side mirrors raw pass-params (`lizenz`, `jid`, `agn`, `connectionnumber`, `ppn`, `poolpartnernummer`, `employeenumber`, `advisorid`, `frab`) into 1-year cookies with NO validation. Alias map confirms multiple input names map to same cookie (`jid|customerid→customerid`, `agn|connectionnumber→agenturnummer`, `ppn|poolpartnernummer→poolpartnernummer`). No CSRF tokens on any forms. Cookies set via `Set-Cookie` with `Max-Age=31536000`; no `Secure`/`HttpOnly`/`SameSite` attributes observed in prior recon. Attacker can craft links that poison victim's funnel cookies, potentially hijacking partner/customer session context or injecting fake advisor/poolpartner identity into downstream comparison/quote flows.
evidence_needed: Confirm cookie attributes (Secure/HttpOnly/SameSite) on Set-Cookie headers; verify downstream endpoints trust cookie values without re-validation; test parameter collision (e.g., `jid=X&customerid=Y` — which wins?).
verify_steps: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET); GET https://kassenkompass.de/bonusrechner.php?jid=X&customerid=Y — observe which cookie value wins (passive); GET https://kassenkompass.de/termin.php with poisoned cookies — observe if identity carries into booking flow (passive, requires cookie jar).
impact: Session fixation / identity injection into insurance comparison funnel; partner/advisor impersonation; downstream quote manipulation; MEDIUM-HIGH.
testability: PASSIVE
[HYP] GTM Proxy Subdomain — Self-Hosted Tag Manager with No Debug Endpoints
class: MISCONFIG
asset: awv.kassenkompass.de
confidence: 45
reasoning: Newly discovered dedicated host `awv.kassenkompass.de` runs self-hosted GTM proxy (nginx) serving `/gtm.js?id=GTM-TT4LBVMW`; root returns 404. Probes confirm `/gtm/debug`, `/gtm/preview`, `/gtm/auth` all return 404 — no standard debug endpoints exposed. `load.awv.kassenkompass.de` returns 403 (Cloudflare challenge). No container config leakage via `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` tested yet.
evidence_needed: Test `/gtm.js?id=GTM-TT4LBVMW&l=dataLayer` for dataLayer config leakage; test CORS on GTM endpoints; verify `load.awv.kassenkompass.de` serves distinct content vs proxy under authenticated session.
verify_steps: GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW&l=dataLayer — probe for dataLayer config (passive); GET https://awv.kassenkompass.de/gtm.js?id=GTM-TT4LBVMW with Origin header — test CORS (passive); GET https://load.awv.kassenkompass.de/ with cookie jar — observe if Cloudflare challenge bypassable (passive).
impact: GTM container config leakage (marketing tags, custom HTML/JS, dataLayer structure) — LOW-MEDIUM; reduced since debug endpoints absent.
testability: PASSIVE
[PARKED] GTM Proxy Subdomain — Self-Hosted Tag Manager with No Debug Endpoints: confidence 45 < 50 threshold; debug/preview/auth endpoints all 404; impact reduced to speculative dataLayer leakage only; no active misconfiguration confirmed.
[FINAL] 1. Funnel Parameter-to-Cookie Injection — Unvalidated PII/Identity Fields Persisted for 1 Year (confidence 70, PASSIVE)
[FINAL] 2. Cross-Version Authorization Bypass — v2 Middleware Accepts v1-Scoped Secrets (confidence 62, PASSIVE mapping + AUTH_HELPED for data diff)
[NEXT] PROBE: GET https://kassenkompass.de/bonusrechner.php?lizenz=test&jid=123&agn=456&ppn=789 — capture Set-Cookie headers (passive, HEAD/GET, 1 rps); GET https://kassenkompass.de/bonusrechner.php?jid=X&customerid=Y — observe parameter collision resolution (passive)
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (15 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /sync/ returns HTTP 200 with auth error in body instead of 401 — behavioral misconfiguration could bypass automated scanners
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Two distinct 403 error messages across endpoints — "ungültig oder nicht berechtigt" (8 endpoints) vs "Ungültiger X-API-Secret" (only /user/{ext_id}) — indicates separate auth middleware stacks with potentially different authorization scopes
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /cat_detail/ catalog says GET but requires POST — catalog inaccuracy, confirms 15-endpoint catalog is structural but not method-authoritative
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: /settlement_report/ returns proper 401/403 RFC 9457 format — consistent with majority of endpoints, no status-code misconfiguration here
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: `/v2/` exposes a distinct versioned router (v2.0 "breite Variante") with `GET /v2/insurance_info/{kk_id}` returning draft categories + resolved references — undocumented in 4+ prior recon sessions; widest per-request data surface on the API
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 unknown paths return structured router-404 oracle (`API-Endpunkt 'v2/X' nicht gefunden`) vs v1's full-catalog catch-all — versioned endpoint enumeration primitive; only `insurance_info` registered so far
[LEARN] ACCEPTED OTHER @ api.kassenkompass.de: v2 router greedy-segment match — `/v2/insurance_info/{anything}` (incl. `/1/extra`, `//1`, `/1/`, `%31`) all reach the protected handler (401); kk_id not validated at routing
[LEARN] REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
[LEARN] REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
[LEARN] REJECTED CORS @ api.kassenkompass.de: No access-control-allow-origin reflection for arbitrary origins — confirmed across sessions
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Password-reset magic `KKX3382745` is not a valid API secret — re-confirmed
[LEARN] REJECTED MISCONFIG @ www.kassenkompass.de: Mirror header drift — www and apex serve identical security headers (XFO SAMEORIGIN, XCTO nosniff, HSTS includeSubDomains, no CSP); AWS ALB backend confirmed; drift hypothesis dropped
[LEARN] ACCEPTED OTHER @ kassenkompass.de: Funnel server mirrors raw pass-params into 1-year cookies (afilcode, customerid, agenturnummer, poolpartnernummer, employeenumber, advisorid, frab) with no validation — alias map jid|customerid→customerid, agn|connectionnumber→agenturnummer, ppn|poolpartnernummer→poolpartnernummer
[LEARN] ACCEPTED OTHER @ kassenkompass.de: New dedicated hosts awv.kassenkompass.de (self-hosted GTM proxy, nginx, /gtm.js?id=GTM-TT4LBVMW, root=404) + load.awv.kassenkompass.de (Cloudflare-challenged) — JS-discovered, supersedes wildcard-DNS "0 dedicated hosts"
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: v2 sweep — insurance_info is the only registered v2 route (24 names → router-404 oracle); single-endpoint versioned surface
[LEARN] ACCEPTED MISCONFIG @ api.kassenkompass.de: Auth map corrected — v1 majority and v2 share middleware A ("Der bereitgestellte X-API-Secret ist ungültig oder nicht berechtigt"); only /user/{ext_id} middleware B ("Ungültiger X-API-Secret" + instance echo); /sync/ legacy HTTP-200 custom JSON; two stacks + one legacy, not three
[LEARN] REJECTED AUTH @ api.kassenkompass.de: No alternate auth channel anywhere — Authorization Bearer, X-API-Key, X-Api-Token, api_key query all 401 "erforderlich"; X-API-Secret sole channel; no header-name bypass
[LEARN] REJECTED CRED_REUSE @ api.kassenkompass.de: Magic KKX3382745 + X8372 rejected (403) on all three auth paths incl. middleware-B and v2 — closed completely
[LEARN] ACCEPTED OTHER @ awv.kassenkompass.de: GTM proxy debug/preview endpoints return 404 — no standard GTM debug surface exposed; root returns 404 not 400
[RISK] kassenkompass: 74 — API catalog disclosure + sensitive endpoints (user data, deletion, financial reports) behind single custom header auth; main funnel handles PII/health data; three privileged login portals; AWS ALB + Cloudflare provides WAF but app-layer authz untested; two-tier auth middleware suggests scoping complexity; v2 router exposes unreleased draft data surface; funnel cookie injection with 1-year persistence and no validation; new GTM proxy subdomain expands attack surface; no public vuln disclosure program visibility beyond bugs.olivermaicher.eu
