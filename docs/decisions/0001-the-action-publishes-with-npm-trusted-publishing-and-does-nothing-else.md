---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - action.yml
  - scripts/publish.sh
  - README.md
---

# The action publishes with npm trusted publishing and does nothing else

## Context and problem statement

npm trusted publishing lets a workflow prove its identity to npm instead of holding a long-lived token. Recorded retroactively from the README, the inputs and `.github/agentic-workflows/scope.md`, which lists publishing with a long-lived token as a decision for a maintainer.

## Decision

- Publishing goes through npm trusted publishing (OIDC). The job needs `id-token: write` and `contents: read`, the package has trusted publishing enabled in npm for the repository and workflow, and the action takes no npm token as input.
- Publishing with a long-lived token, or to a registry other than npm, needs a maintainer's decision.
- The action does not compute versions, update manifests, run preflight checks, or create tags and releases. Those are other actions: version-bump-action (computes the version), release-preflight-action (checks collisions and drift), manifest-version-update-action (writes the version), ai-changelog-action (writes the changelog) and npm-trusted-publish-action (publishes).

## Consequences

- Each package is set up in npm once, and the workflow that publishes must be the one registered there.
