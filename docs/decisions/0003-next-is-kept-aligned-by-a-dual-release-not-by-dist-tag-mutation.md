---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/publish.sh
  - action.yml
  - README.md
---

# next is kept aligned by a dual release, not by dist-tag mutation

## Context and problem statement

After a stable release the `next` channel should not point at an older prerelease. The first implementation moved the dist-tag itself (fetching and setting dist-tags, with a `dist-tag-token` input for a granular npm write token, commits 65d8940 and 6f03461) and was replaced by dual release on the same day (39580b9, 8026157). Recorded retroactively.

## Decision

- With `dual-release-on-stable: true` and a stable release type, the action publishes a companion prerelease `x.y.z-n` to `next` and then the stable `x.y.z` to `latest`.
- `companion-prerelease-version` sets the companion version; without it the action takes the next numeric prerelease counter from npm.
- The option is off by default. The action does not run `npm dist-tag`.

## Consequences

- A stable release creates one more version on npm. Outputs report the companion separately (`companion_prerelease_published`, `companion_prerelease_version`).

## Alternatives considered

Mutating the dist-tag with a granular write token: replaced the same day. The README says the dual release "keeps `next` aligned without relying on `npm dist-tag add`".
