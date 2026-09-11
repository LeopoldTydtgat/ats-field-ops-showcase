# ADR 0005: Signed release builds only for the team; debug and release keys separated

**Status:** accepted, learned the hard way.

## Context

The app is sideloaded, not distributed via the Play Store. Android refuses to install an APK over an existing app signed with a different key (`INSTALL_FAILED_UPDATE_INCOMPATIBLE`). Debug builds use a different signing key than release builds.

## Decision

The team only ever receives proper signed release builds. Debug builds stay on my own device. The release keystore is backed up, because losing it would permanently break the update path.

## Consequences

- Updates install cleanly over the previous version and local data persists.
- No accidental debug-signed APK can strand a user's phone mid-update.
- Keystore custody is treated as an operational responsibility, not an afterthought.
