<!-- markdownlint-disable -->

# Hardening Report: ppremk--lfs-warning/v3.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ppremk--lfs-warning/v3.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow main.yml references GitHub Actions using mutable version tags instead of full 40-character SHA commit digests. This exposes the workflow to supply-chain attacks if the tag is moved to a different (potentially malicious) commit. Failing references: `actions/checkout@v3` (line 19) and `actions/setup-node@v3` (line 21). Note: pr-check.yml correctly pins both actions to full SHAs.

Locations:

- `.github/workflows/main.yml:19`
- `.github/workflows/main.yml:21`

### missing-permissions (severity: medium)

Neither main.yml nor pr-check.yml defines a top-level `permissions:` key, and no job in either file has a job-level `permissions:` block. Without explicit permissions, workflows inherit the default repository permissions (which may be overly broad, e.g. write access to contents). Each workflow should declare the minimal permissions required.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/pr-check.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed main.yml: pinned actions/checkout@v3 → @a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3 and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 # v3. Added top-level permissions block to main.yml (contents: read, pull-requests: write) since the LFS warning action posts PR comments. Added top-level permissions block to pr-check.yml (contents: read) since it only checks out and builds code. pr-check.yml already had both actions pinned to full SHAs so no changes were needed there for unpinned-uses.

