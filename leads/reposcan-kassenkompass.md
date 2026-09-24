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
## REPOSCAN 2026-09-12 14:12:38 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 17:14:47 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 19:26:30 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 21:47:35 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-12 23:34:24 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 01:17:50 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 06:18:31 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 12:02:11 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 16:25:46 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 18:56:52 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 21:14:54 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-13 23:13:22 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-14 01:11:47 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-14 06:24:21 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-14 13:18:33 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-14 18:43:14 UTC
[HYP] REPOSCAN-EMPTY — Zero public repositories for KassenKompass
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
impact: None — source-code secret surface is empty; no hardcoded credentials, API keys, cloud
verify_steps: Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone;
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-14 22:15:38 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 00:42:34 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 05:47:51 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 11:03:03 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 11:58:00 UTC
[HYP] REPOSCAN-EMPTY — Zero public repositories for KassenKompass
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
  KassenKompass-GmbH (GitHub org id 316947552) exists but has 0 public repositories.
  KassenKompass (no suffix) returns HTTP 404 — no such org.
  Unauthenticated GitHub API confirmed both: GET /orgs/KassenKompass-GmbH/repos → 200 + empty [];
  GET /orgs/KassenKompass/repos → 404.
  cands.txt = "no org candidates"; scope.yml github_orgs = "none-configured".
  No candidate source code is publicly accessible for cloning, grep, or static analysis.
impact: N/A — source-code secret surface is empty; no hardcoded credentials, API keys, cloud
  creds, or insecure code patterns can be discovered in repos that do not exist.
verify_steps: |
  Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone;
  no active scan needed. Match 13 prior scan entries reporting identical finding.
## REPOSCAN 2026-09-15 15:36:58 UTC
[HYP] REPOSCAN-EMPTY — Zero public repositories for KassenKompass
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
impact: N/A — source-code secret surface is empty; no hardcoded credentials, API keys, cloud
verify_steps: |
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 19:11:09 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-15 22:18:58 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 00:30:14 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 05:12:16 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 10:01:17 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 15:01:13 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 18:56:15 UTC
[HYP] REPOSCAN-EMPTY — Zero public repositories for KassenKompass
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
impact: N/A — source-code secret surface is empty; no hardcoded credentials, API keys, cloud
verify_steps: |
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-16 21:54:16 UTC
[HYP] No public source code available for audit
class: OTHER
asset: n/a
confidence: 100
reasoning: KassenKompass-GmbH has 0 public GitHub repos; no candidate org repos exist to audit. Workspace grep for AKIA*, AIza*, ghp_*, sk_live_*, -----BEGIN PRIVATE, password=, api_key, secret, token, client_secret, s3/google/azure bucket URLs — all zero true positives.
impact: N/A
verify_steps: Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone; no active scan needed.
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 00:04:15 UTC
[HYP] No public repos in scope for source-code secret scan
class: OTHER
asset: github.com/KassenKompass-GmbH
confidence: 100
reasoning: GitHub API confirms 0 public repos on the KassenKompass-GmbH org. scope.yml also lists no configured GitHub orgs. cands.txt reads "no org candidates".
impact: None — no source artifacts to yield secrets
verify_steps: curl -s "https://api.github.com/orgs/KassenKompass-GmbH" | jq '.public_repos'
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 04:59:12 UTC
[HYP] No public repos in scope for source-code secret scan
class: OTHER
asset: N/A (KassenKompass-GmbH has 0 public GitHub repos)
confidence: 100
reasoning: scope.yml github_orgs=none-configured; cands.txt="no org candidates"; reposcan-raw/summary.txt confirms TARGET_ORG empty; unauthenticated GitHub API search yielded 0 org-owned repos; workspace grep for AKIA*, AIza*, ghp_*, sk_live_*, -----BEGIN PRIVATE, password=, api_key, secret, token, client_secret, s3/google/azure bucket URLs returned zero true positives across all .md/.json/.txt files
impact: None — no source artifacts to yield secrets
verify_steps: Passively confirmed via unauthenticated GitHub API (no auth token). No repos to clone; no active scan needed.
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 09:55:48 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 14:41:11 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 18:48:32 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 21:55:23 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-17 23:54:52 UTC
[HYP] (none)
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 03:10:11 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 08:20:35 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 13:01:59 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 17:06:50 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 19:41:45 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-18 22:17:47 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 00:25:13 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 05:01:10 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 09:23:58 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 13:24:59 UTC
[HYP] REPOSCAN-EMPTY — Zero public repositories for KassenKompass
class: OTHER
asset: github.com/orgs/KassenKompass-GmbH (0 public repos)
confidence: 100
reasoning: |
impact: None — no source artifacts to yield secrets, hardcoded creds, or insecure patterns
verify_steps: |
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 16:47:14 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 19:10:06 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 21:30:25 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-19 23:29:45 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 01:35:09 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 06:57:58 UTC
[HYP] REPOSCAN-EMPTY — No public repositories available for source-code audit
class: OTHER
asset: N/A
confidence: 100
reasoning: |
impact: N/A — source-code secret surface is empty; no hardcoded credentials, API keys, cloud
verify_steps: |
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 12:06:13 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 16:13:22 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 18:52:14 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 21:09:56 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-20 23:16:58 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-21 01:13:21 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-21 06:27:44 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-21 13:18:31 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-21 18:48:05 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-21 22:26:01 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 01:07:22 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 06:19:36 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 11:51:42 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 16:15:24 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 19:46:15 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-22 22:43:18 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 01:14:30 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 06:03:18 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 11:46:32 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 16:04:58 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 19:42:15 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-23 22:40:08 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
## REPOSCAN 2026-09-24 00:54:06 UTC
TARGET_ORG not configured for kassenkompass; skipping public-org deep scan.
