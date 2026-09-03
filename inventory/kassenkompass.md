# KassenKompass GmbH inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
api.kassenkompass.de
kassenkompass.de
www.kassenkompass.de

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 3 hosts | **Live HTTP:** 0

| Host | Status | Server/Tech |
|---|---|---|

## 2026-09-02 21:45:31 UTC

## 2026-09-02 23:58:49 UTC

## 2026-09-03 04:13:45 UTC

## 2026-09-03 09:04:36 UTC

## 2026-09-03 13:34:54 UTC

## 2026-09-03 17:32:49 UTC
- NEW api.kassenkompass.de — live REST API, 16 endpoints enumerated, X-API-Secret auth, `/health/` unprotected, full API docs returned at ALL paths (/, /admin/, /debug/, /swagger/, /openapi.json)
- NEW kassenkompass.de — live frontend, Cloudflare-fronted, insurance comparison platform with customer/partner/insurer logins
- NEW www.kassenkompass.de — mirrors kassenkompass.de
- CHANGED Inventory Live HTTP count: 0 → 3 (all three hosts serve HTTP)
