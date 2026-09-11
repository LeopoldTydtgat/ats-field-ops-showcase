# ADR 0006: Gemini voice typing with SHA-1 key restriction at release

**Status:** accepted, verified against production code and cloud console.

## Context

Field users dictate faster than they type. Voice input calls the Gemini API for transcription and parsing, which means an API key ships inside a sideloaded APK.

## Decision

Restrict the API key in Google Cloud to Android apps: the app's package ID and the release signing certificate's SHA-1 fingerprint, with API access limited to the Gemini API only. The app sends `X-Android-Package` and `X-Android-Cert` headers with every request so Google can enforce the restriction.

## Consequences

- A key extracted from the APK is useless outside the genuine signed app.
- The restriction is tied to the release certificate, which reinforces the release-only distribution rule in ADR 0005.
- The key cannot be repurposed for any other Google API.
- No fingerprints or key values appear anywhere in this showcase.
