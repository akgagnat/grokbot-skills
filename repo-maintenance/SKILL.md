---
name: repo-maintenance
description: >-
  Use when updating dependencies, applying security patches, reviewing update
  PRs, merging them, or checking deploys in the user's GitHub repos.
---
# Repo maintenance: update, review, merge, verify

The policy and procedure for keeping the user's repos up to date. The repo list, schedule and reporting channel live in the routine that runs this (e.g. the weekly dependency routine).

## Hard rules
- Never merge a PR unless the user explicitly asked for that merge in chat (or a saved routine prompt names exactly that merge). Record each merge request in the journal.
- Never enable on-demand usage. Use included models (e.g. grok-4.6) for cloud agents, and continue on an included model if a usage limit is hit.
- When verifying an app, don't write large amounts of data; use read-only health checks. Don't log in or open owner-only dashboards.
- Skip repos the user marked undeployed/retired (check memory).

## Version policy
- Node: stay on the current LTS major (Node 24 as of 2026). No non-LTS majors.
- Databases in CI, tests and Compose stay on the same major as production. For Postgres, production's version is in the infra repo's Terraform (`postgres_version`). MongoDB repos stay on their current major unless the user asks.
- Prefer patch and minor updates. Take a major only when build and tests pass; otherwise list it as needing manual attention.
- Fresh releases normally wait out the repo's release-age gate (~24h), but CVE/security fixes may be taken immediately if tests and review pass.

## 1. Update
- One cloud agent (default model) per repo, one PR per repo, on a new branch. If an earlier update PR is still open, update that instead of opening a duplicate.
- Cover all manifests: package.json/lockfiles, Docker base images, GitHub Actions, Go, Gradle.
- Run install (frozen lockfile), lint, typecheck, build, unit tests and e2e where present.
- PR description: what changed, majors and breaking changes, what was held back and why.

## 2. Independent review
- A second cloud agent on a different model than the updater reviews each PR critically: breaking changes per major, untested behaviour changes, runtime/config drift from production, lockfile sanity, coverage of changed paths, e2e.
- Security scanning:
  - `trivy image --severity HIGH,CRITICAL` on images built from the branch, and `trivy fs` on the repo. Compare with main to separate new from pre-existing findings.
  - `zizmor .github/workflows` for unpinned actions, broad permissions/tokens, template injection.
  - Fix new high/critical findings that are safe to fix on the branch; list the rest.
- Reviewer posts a PR comment, pushes real fixes, reruns checks, adds a "Review" section to the PR description with a merge-readiness verdict. It never merges.

## 3. Report
- In the user's language (Norwegian), one line per repo: PR link, verdict, notable scan findings, what still needs attention. Stay quiet if nothing needed updating.

## 4. Merge (only when asked)
- For each PR: confirm open, mergeable, CI green, and that the head SHA equals the reviewed SHA. If the head moved or CI is red, don't merge; report why.
- Squash-merge with a SHA guard.

## 5. Verify deploy
- Watch the deploy workflow triggered by each merge commit on the default branch until it finishes.
- Then do light GET health checks (`/health`, `/healthz`, `/readyz`). A 401 from an auth sidecar on `/` is expected without a session.
- Cluster API (kubectl) is not reachable from the bot's computer; rely on Actions status and HTTP checks.
- Report per repo: merge commit, deploy result with link, health results, anything failing.
