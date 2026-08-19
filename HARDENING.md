<!-- markdownlint-disable -->

# Hardening Report: ppremk--lfs-warning/v2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ppremk--lfs-warning/v2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v2`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated or compromised without the workflow noticing, enabling supply-chain attacks. It should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`.

Locations:

- `.github/workflows/main.yml:19`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `lfs-warning` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which may include broad write access). A minimal permissions block such as `permissions: contents: read` should be added.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v2` to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with `# v2` comment for readability. 2. Added top-level `permissions: contents: read` block — the minimum needed for the checkout step to clone the repository.

