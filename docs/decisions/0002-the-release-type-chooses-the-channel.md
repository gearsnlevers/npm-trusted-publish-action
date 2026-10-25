---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/publish.sh
  - action.yml
issues:
  - vscheuber/npm-trusted-publish-action#1
---

# The release type chooses the channel

## Context and problem statement

Prereleases must not become the default install, and stable releases must. Recorded retroactively from the README and #1.

## Decision

- `prerelease` and `premajor` publish to the `next` tag and report `is-prerelease=true`. `patch`, `minor` and `major` publish to `latest`. `tag-override` sets the tag explicitly. Any other release type fails.
- `premajor` (a prerelease of the next major, such as `5.0.0-1`) is treated exactly like `prerelease`, including skipping the dual-release path below.

## Consequences

- The output `tag` says which channel was used.
