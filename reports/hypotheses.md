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
