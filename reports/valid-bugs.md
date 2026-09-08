# Validated findings (running count 0)

- 1 lead(s) marked VALID at 2026-09-04 19:20:31 UTC
  - | **VALID** | 2 | API Catalog Disclosure (MISCONFIG, CVSS 5.3), /sync/ 200 Misconfig (MISCONFIG, CVSS 5.3) |

- 13 lead(s) marked VALID at 2026-09-06 05:06:57 UTC
  - | Q5 Novel? | **DUPLICATE** — already accepted 2026-09-04 19:20 UTC in valid-bugs.md |
  - | Q3 Impact? | **YES** — attacker with valid API secret reads any user's PII (name, insurance, email, address); GDPR-relevant |
  - | Q4 Provable? | **NO** — requires valid X-API-Secret (AUTH_HELPED); no passive verification possible |
  - **Verdict: HOLD** — Requires valid X-API-Secret to verify. Cannot prove non-invasively. Revisit when scoped test credentials obtained.
  - | Q4 Provable? | **NO** — error shape mapping is passive, but confirming actual scope confusion requires valid key (AUTH_HELPED) |
  - **Verdict: HOLD** — Architectural signal only. Cannot confirm exploitability without valid X-API-Secret. Revisit when credentials obtained.
  - | Q3 Impact? | **YES** — attacker with valid secret deletes any user's data |
  - | Q4 Provable? | **NO** — requires valid X-API-Secret; destructive endpoint (no safe passive verification) |
  - **Verdict: HOLD** — Requires valid X-API-Secret + destructive testing. Cannot prove non-invasively.
  - | Q4 Provable? | **NO** — requires valid scoped X-API-Secret |
  - **Verdict: HOLD** — Requires valid X-API-Secret. Revisit with scoped credentials.
  - **Verdict: VALID**
  - | 14 | **Funnel cookie-stuffing** | **VALID** ✅ |

- 8 lead(s) marked VALID at 2026-09-07 23:19:50 UTC
  - **VERDICT: VALID**
  - | Q2 Reachable | NO | Requires valid X-API-Secret; unauth returns 401 |
  - | Q4 Provable | NO | Cannot verify without valid API secret |
  - | Q2 Reachable | NO | Requires valid X-API-Secret |
  - | Q4 Provable | NO | Requires valid key + destructive testing |
  - | Q2 Reachable | NO | Requires valid X-API-Secret |
  - | Q4 Provable | NO | Cannot verify without valid scoped secret |
  - | 1 | Unauthenticated API Catalog Disclosure | **VALID** | 5.3 | Submit to bugs.olivermaicher.eu |

- 19 lead(s) marked VALID at 2026-09-08 21:38:18 UTC
  - | Q5 Novel/unreported? | **DUPLICATE** — already accepted 2026-09-04 19:20 UTC in valid-bugs.md |
  - | Q2 Reachable? | **NO** — requires valid X-API-Secret (auth-gated, returns 401 without it) |
  - | Q4 Provable non-invasively? | **NO** — requires valid API key to demonstrate cross-user access |
  - **Verdict: HOLD** — Requires valid X-API-Secret to verify. Revisit when scoped test credentials obtained.
  - | Q2 Reachable? | **NO** — requires valid X-API-Secret |
  - | Q4 Provable non-invasively? | **NO** — requires valid key + destructive endpoint (no safe passive verification) |
  - **Verdict: HOLD** — Requires valid X-API-Secret + destructive testing. Cannot prove non-invasively.
  - | Q2 Reachable? | **NO** — requires valid X-API-Secret |
  - | Q4 Provable non-invasively? | **NO** — requires valid scoped secret |
  - **Verdict: HOLD** — Requires valid X-API-Secret. Revisit with scoped credentials.
  - | Q2 Reachable? | **PARTIAL** — error shape observable unauthenticated; scoping differential requires valid key |
  - | Q4 Provable non-invasively? | **NO** — passive mapping confirms architecture but cannot confirm exploitability without valid key |
  - **Verdict: HOLD** — Cannot confirm exploitability without valid X-API-Secret. Revisit when credentials obtained.
  - | Q2 Reachable? | **PARTIAL** — catalog mismatch observable unauth; POST behavior requires valid key |
  - **Verdict: VALID**
  - | 3 | IDOR /user/{ext_id} | **HOLD** | Needs valid X-API-Secret |
  - | 4 | BOLA /delete/{id} | **HOLD** | Needs valid X-API-Secret |
  - | 5 | BOLA /settlement_report | **HOLD** | Needs valid X-API-Secret |
  - | 12 | Funnel Cookie-Staffing | **VALID** | CVSS 6.5, submit to bugs.olivermaicher.eu |
