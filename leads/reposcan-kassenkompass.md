## REPOSCAN 2026-09-03 15:47:08 UTC
[HYP] No candidate repositories identified for audit
class: OTHER
asset: n/a
confidence: 100
reasoning: cands.txt contains "no org candidates"; scope.yml lists github_orgs: "none-configured"
impact: N/A
verify_steps: N/A - no repos to scan
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-03 19:05:42 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-03 21:44:46 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-03 23:46:34 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 02:53:05 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 07:42:47 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 12:29:44 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 16:35:45 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 19:10:24 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 21:33:50 UTC
[HYP] No candidate repositories identified for source-code audit
class: OTHER
asset: n/a
confidence: 100
reasoning: cands.txt contains "no org candidates"; scope.yml lists github_orgs: "none-configured"; GitHub API returns 404 for KassenKompass org (case-insensitive); no public GitHub org exists under this name
impact: N/A — source-code secret scan surface is empty
verify_steps: N/A — nothing to confirm; the org either has no public GitHub repos or uses a different org name
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-04 23:17:29 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 01:05:05 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 05:50:32 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 09:57:07 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 13:16:48 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 16:07:54 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 18:22:44 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 20:43:01 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-05 22:38:16 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 00:13:50 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 04:47:14 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 09:09:27 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 12:56:26 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 15:58:51 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 18:09:58 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 20:28:53 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-06 22:18:52 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 00:03:40 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 04:50:42 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 09:56:54 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 15:33:57 UTC
[HYP] N/A — No public repos in scope
class: N/A
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: GitHub API confirms the org "KassenKompass-GmbH" (id 316947552) exists but has zero public repositories. No source code is publicly available to audit.
impact: None
verify_steps: GET https://api.github.com/orgs/KassenKompass-GmbH/repos → returns empty array []
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 19:23:55 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-07 22:17:11 UTC
[HYP] No public source code available for audit
class: OTHER
asset: n/a
confidence: 100
reasoning: KassenKompass-GmbH has 0 public repos on GitHub; no candidate org repos exist to clone and grep for secrets/credentials.
impact: N/A — no source-code secret surface to report
verify_steps: GET https://api.github.com/orgs/KassenKompass-GmbH/repos → []
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 00:28:18 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 05:11:09 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 09:48:05 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 14:08:08 UTC
[HYP] No public repositories available for source-code audit
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH
confidence: 100
reasoning: KassenKompass-GmbH (GitHub org id 316947552) exists but has 0 public repositories. GitHub API confirmed: GET /orgs/KassenKompass-GmbH/repos returns empty []. GET /orgs/KassenKompass/repos returns 404 (no such org). GET /users/olivermaicher/repos returns 404. No candidate source code is publicly accessible for cloning, grep, or static analysis.
impact: None — source-code secret surface is empty; no hardcoded credentials, API keys, cloud creds, or insecure code patterns can be discovered in repos that do not exist.
verify_steps: Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone; no active scan needed.
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 17:57:22 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 20:51:41 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-08 23:11:29 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 01:17:26 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 06:05:20 UTC
[HYP] REPOSCAN-EMPTY
class: OTHER
asset: N/A
confidence: 100
reasoning: KassenKompass-GmbH has 0 public GitHub repos; no org candidates exist to audit. Workspace grep for AKIA*, AIza*, ghp_*, sk_live_*, -----BEGIN PRIVATE, password=, api_key, secret, token, client_secret, s3/google/azure bucket URLs — all zero true positives.
impact: N/A — no source-code secret surface
verify_steps: Unauthenticated GitHub API: GET https://api.github.com/orgs/KassenKompass-GmbH/repos → empty array. Workspace grep confirmed clean.
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 11:32:38 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 15:18:05 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 18:41:32 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 21:30:33 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-09 23:30:00 UTC
[HYP] REPOSCAN-EMPTY — No public source code available for audit
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: KassenKompass-GmbH exists but has zero public repositories. GitHub API confirmed via unauthenticated GET /orgs/KassenKompass-GmbH/repos → empty array. No candidate source code is publicly accessible for cloning, grep, or static analysis.
impact: N/A — no source-code secret surface
verify_steps: Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone; no active scan needed.
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 01:26:20 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 06:38:38 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 11:48:56 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 15:50:01 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 18:56:12 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 21:25:42 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-10 23:22:51 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 01:26:31 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 06:37:20 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 11:48:27 UTC
[HYP] REPOSCAN-EMPTY — Zero public repos for KassenKompass-GmbH
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
impact: N/A — source-code secret surface is empty
verify_steps: |
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 15:58:13 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 18:57:59 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 21:37:29 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-11 23:31:55 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 01:31:09 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 06:28:55 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 11:14:52 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
