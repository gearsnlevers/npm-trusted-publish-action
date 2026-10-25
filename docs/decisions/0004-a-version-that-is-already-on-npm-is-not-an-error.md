---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/publish.sh
  - README.md
---

# A version that is already on npm is not an error

## Context and problem statement

Recorded retroactively from commit eda5349 and the README. The motivation is not written down; the behaviour is what a rerun of a partly finished release sees.

## Decision

- When `package-name` and `version` are given and that exact version is on npm, the action skips `npm publish` and succeeds with `already-published=true` (recovery mode).
- With dual release the stable and the companion versions are each checked and reported on their own (`stable_already_published`, `companion_prerelease_already_published`).

## Consequences

- A repeated run is safe. It cannot repair a version that was published with the wrong content.
