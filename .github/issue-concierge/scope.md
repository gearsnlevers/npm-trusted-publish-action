# Project scope

Read by the issue gate's scope check (Repo Concierge). The check is off for a repository without this file.

## Purpose

Publish npm packages with trusted publishing (OIDC), with release-type aware channel selection (`next` or `latest`), recovery when a version is already published, and an optional dual publish for stable releases.

## In scope

- Publishing to npm through trusted publishing (OIDC)
- Selecting the dist-tag from the release type, including the companion prerelease on stable releases
- Recovery mode when the exact version is already on npm, and dry runs
- The action's inputs and outputs, documentation, tests, and release pipeline

## Out of scope

<!-- Every item here can close an issue automatically as not planned. Keep the list short and specific. -->

- Computing versions, updating manifests, running preflight checks, or creating git tags and GitHub releases. The action only publishes; the surrounding release workflow handles those steps.

## Needs a maintainer

- Publishing with a long-lived npm token instead of trusted publishing
- Registries other than npm

## Where to go instead

- Computing versions: version-bump-action. Updating manifests: manifest-version-update-action. Preflight checks: release-preflight-action.
