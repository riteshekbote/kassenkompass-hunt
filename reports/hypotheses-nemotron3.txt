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
