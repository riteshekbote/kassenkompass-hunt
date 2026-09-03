# Knowledge Base (seed)
- 2026-09-03 ACCEPTED MISCONFIG @ api.kassenkompass.de: Root endpoint discloses full API catalog (14 endpoints) without auth — violates principle of least privilege, enables targeted attack planning
- 2026-09-03 REJECTED SSRF @ api.kassenkompass.de: No evidence of user-supplied URLs, webhook handlers, or fetch mechanisms in catalog; no cloud metadata exposure path identified
- 2026-09-03 REJECTED JWT_ALG_CONFUSION @ api.kassenkompass.de: Auth uses custom X-API-Secret header, not JWT — class not applicable
