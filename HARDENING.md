<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-gke-credentials/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--get-gke-credentials/v3.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions or reusable workflows using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit.

Failing references:
- `.github/workflows/draft-release.yml` line 17: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'`
- `.github/workflows/integration.yml` line 30: `uses: 'google-github-actions/auth@v3'`
- `.github/workflows/integration.yml` line 55: `uses: 'google-github-actions/auth@v3'`
- `.github/workflows/release.yml` line 11: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'`
- `.github/workflows/unit.yml` line 40: `uses: 'google-github-actions/auth@v3'`

All are annotated with `# ratchet:exclude`, indicating they are intentionally excluded from automated pinning, but they remain unpinned and must be replaced with full SHA digests.

Locations:

- `.github/workflows/draft-release.yml:17`
- `.github/workflows/integration.yml:30`
- `.github/workflows/integration.yml:55`
- `.github/workflows/release.yml:11`
- `.github/workflows/unit.yml:40`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 5 unpinned action references to full commit SHAs:
- `.github/workflows/draft-release.yml` line 17: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
- `.github/workflows/integration.yml` line 30: `google-github-actions/auth@v3` → `@7c6bc770dae815cd3e89ee6cdf493a5fab2cc093 # v3`
- `.github/workflows/integration.yml` line 55: `google-github-actions/auth@v3` → `@7c6bc770dae815cd3e89ee6cdf493a5fab2cc093 # v3`
- `.github/workflows/release.yml` line 11: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
- `.github/workflows/unit.yml` line 40: `google-github-actions/auth@v3` → `@7c6bc770dae815cd3e89ee6cdf493a5fab2cc093 # v3`

SHAs were resolved using lookup_action_sha. The `# ratchet:exclude` comments were replaced with `# v3` to preserve readability while removing the mutable tag references.

