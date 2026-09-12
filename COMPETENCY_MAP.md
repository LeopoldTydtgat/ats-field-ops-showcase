# Competency Mapping: ATS Field Ops App

How this production build maps to cloud and IT competencies.

| App feature | What I did | Competency |
|---|---|---|
| Email OTP login, invite-only | Configured Supabase Auth with signups disabled and a two-account whitelist; session persistence with refresh tokens | Identity and access management |
| Row Level Security on every table | Wrote and tested RLS policies; verified the anonymous role has zero access | Data security, least privilege |
| Realtime sync between two phones | Subscribed both devices to Postgres changes; chose and documented a reload strategy sized to actual scale (ADR 0003) | Distributed state, pragmatic architecture |
| Kit snapshots on job attach | Designed immutable JSONB snapshots so historical records survive template edits (ADR 0001) | Data modelling, auditability |
| Offline cache with banner | SQLite cache updated on every successful read; graceful degradation when the network drops | Resilience, offline-first thinking |
| Local notification scheduling | Deterministic ID scheme from job UUIDs (ADR 0002); timezone-correct scheduling for Africa/Johannesburg; runtime permission handling on Android 13+ | Mobile platform internals |
| OEM notification failure on one device | Diagnosed a Huawei alarm-killing behaviour as a platform limitation, not a code bug; documented the finding and the FCM-based fix path | Incident-style debugging, root cause analysis |
| Signed release distribution | Keystore management, debug/release key separation, sideload update path via WhatsApp (ADR 0005) | Release management |
| API key hygiene | SHA-1 and package restricted Gemini key inside a sideloaded APK (ADR 0006) | Secrets and key management |
| Free-tier keepalive | GitHub Actions cron pinging the database daily to prevent project pause | Automation, cloud cost awareness |
| Pinned dependencies | Exact versions only, deliberate upgrades (ADR 0007) | Supply chain discipline, reproducible builds |
| PDF and CSV exports | Rolled-up materials and tools exports feeding the client's separate invoicing system | Systems integration thinking |
