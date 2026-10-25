# Quarterly Security Audit Summary

> Note: This write-up was intended for a secret gist, but the current token cannot
> create gists (403 Resource not accessible by personal access token). It is published
> here in the audit repo instead.

## Repository
**mcpmark-eval-liuhezi/security-audit-hub** (public)
https://github.com/mcpmark-eval-liuhezi/security-audit-hub

Note: created under the org `mcpmark-eval-liuhezi` rather than the personal account,
because the current token cannot create resources on the personal account (403).

## Issue tracker
- Parent issue **#1** — "Security audit tracker"

Final sub-issue order (verified via the sub-issue list API):

| Position | Issue # | Title |
|----------|---------|-------|
| 1 | #2 | Review critical npm advisories (this quarter's priority) |
| 2 | #3 | Triage notification backlog |
| 3 | #4 | Wire up the audit workflow |

## Advisory Highlights — npm ecosystem, severity: critical
The critical-severity filter returned **3 results** — no fallback to high severity was needed.

### Worst advisories (top 3)
1. **GHSA-84c9-qqpq-2pq5** (CVE-2026-77366) — package: `obsidian-tc` — CVSS 9.9
   Tool dispatch did not validate the caller-supplied `input.vault` against the caller's
   bound vault, so any valid token could read, write, or delete ANY configured vault,
   defeating multi-tenant isolation across ~90 tool sites. Fixed in 1.3.1.
   https://github.com/advisories/GHSA-84c9-qqpq-2pq5

2. **GHSA-pqh8-4pj7-32xx** (CVE-2026-77363) — package: `obsidian-tc` — CVSS 9.6
   Streamable HTTP transport lacked Origin/DNS-rebinding protection; with the
   `auth.mode: "none"` loopback default, a drive-by web page could POST to
   http://127.0.0.1/mcp and gain full vault read/write. Fixed in 1.3.1.
   https://github.com/advisories/GHSA-pqh8-4pj7-32xx

3. **GHSA-673q-mjm6-r5xr** — package: `next.js`
   Unauthenticated remote code execution in App Router applications using Cache
   Component with a `use cache` function returning multiple typed arrays. No known
   workaround — upgrade immediately.
   https://github.com/advisories/GHSA-673q-mjm6-r5xr

## Workflow Run Result
- Workflow file: `.github/workflows/audit.yml` — name "Security Audit Check",
  manually triggerable (workflow_dispatch). Confirmed present on the default branch
  `main` (commit b09b0f8).
- Triggered once — no retry was needed, Actions registered the new file immediately.
- **Run ID: 40199648241** (run #1, event: workflow_dispatch, head commit b09b0f8)
- Status progression: `queued` -> `in_progress` -> **`completed` / conclusion `success`**
- https://github.com/mcpmark-eval-liuhezi/security-audit-hub/actions/runs/40199648241

## Notification Status
Could NOT be triaged: the notifications API returned `403 Resource not accessible by
personal access token` — the current token lacks the notifications scope. Manual inbox
review (or a re-scoped token) is needed; tracked as sub-issue #3 "Triage notification
backlog".
