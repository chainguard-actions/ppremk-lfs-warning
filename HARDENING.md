<!-- markdownlint-disable -->

# Hardening Report: ppremk--lfs-warning/v3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ppremk--lfs-warning/v3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references 'actions/checkout@v2', which uses a mutable tag rather than a full 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling a supply-chain attack. Pin the reference to an immutable SHA, e.g. 'actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2'.

Locations:

- `.github/workflows/main.yml:18`

### missing-permissions (severity: medium)

The workflow file '.github/workflows/main.yml' has no top-level 'permissions:' key, and the only job ('lfs-warning') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Add a top-level 'permissions:' block with the minimal scopes required (e.g. 'contents: read' and 'pull-requests: write' if PR comments are needed).

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v2` to its full commit SHA `ee0669bd1cc54295c223e0bb666b733df41de1c5` with a `# v2` comment for readability. 2. Added a top-level `permissions:` block with `contents: read` (needed for checkout) and `pull-requests: write` (needed for the LFS warning action to post PR comments), replacing the default broad GITHUB_TOKEN permissions.

