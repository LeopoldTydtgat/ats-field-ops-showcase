# ADR 0007: Pinned dependency versions, no caret ranges

**Status:** accepted.

## Context

Flutter's default is caret version ranges (`^`), which allow silent minor upgrades on any `pub get`. Previous AI-assisted builds elsewhere had broken from exactly this kind of drift.

## Decision

Every dependency in `pubspec.yaml` is pinned to an exact version. Upgrades happen deliberately, one at a time, with the change tested before release.

## Consequences

- Builds are reproducible. The APK the team runs is built from known versions.
- No dependency changes ride along as a side effect of unrelated work.
- The cost is manual upgrade work, which is acceptable for a stable production app.
