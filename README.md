# ATS Field Ops: Android App Showcase

![Flutter](https://img.shields.io/badge/Flutter-stable-02569B?logo=flutter)
![Supabase](https://img.shields.io/badge/Supabase-Postgres%20%2B%20Auth%20%2B%20Realtime-3FCF8E?logo=supabase)
![Android](https://img.shields.io/badge/Android-signed%20release-3DDC84?logo=android)
![Status](https://img.shields.io/badge/status-live%20in%20production-E63946)

A small auto-electrical team in Johannesburg was running jobs off memory and paper. Technicians arrived on site missing parts, there was no proof that work had been completed, and the office phoned the owner for every job detail. I designed, built and shipped an Android app solo for **Auto Tech Support** that fixed all three, and it has been in daily production use since June 2026.

[Read the full case study](CASE_STUDY.md)

This repository is a curated showcase. The production repository is private, and every screenshot and video here uses seeded test data because real job records contain customer names.

## Tech stack

| Layer | Choice |
|---|---|
| App | Flutter (Dart), single signed-release APK |
| Auth | Supabase email OTP, invite-only whitelist |
| Database | Supabase Postgres with Row Level Security |
| Sync | Supabase Realtime |
| Offline | Local SQLite cache with offline banner |
| Notifications | Local scheduled notifications (no FCM) |
| Voice input | Gemini API transcription, SHA-1 restricted key |
| Exports | PDF and CSV via system share sheet |
| Ops | GitHub Actions keepalive for the free-tier backend |

## Demo

![ATS demo](docs/ats-demo.gif)

**Full walkthrough (2 minutes):** https://www.youtube.com/watch?v=pTQCMCLtmF4

Recorded on device with seeded test data.

## Architecture

```mermaid
flowchart LR
    A[Flutter Android app] -->|email OTP| B[Supabase Auth]
    A -->|reads and writes| C[(Postgres + RLS)]
    C -->|Realtime events| A
    A --> D[Local SQLite cache]
    A --> E[Local notification scheduler]
    A -->|voice typing| F[Gemini API]
    A --> G[PDF / CSV export to share sheet]
    H[GitHub Actions keepalive] --> C
```

## Screenshots

Seeded test data only.

| | | |
|---|---|---|
| <img src="docs/screenshots/01-kits-list.jpg" width="230"><br>**Kits list** | <img src="docs/screenshots/02-kit-detail.jpg" width="230"><br>**Kit detail** | <img src="docs/screenshots/03-kit-pdf-export.jpg" width="230"><br>**Exported kit PDF** |
| <img src="docs/screenshots/04-jobs-list.jpg" width="230"><br>**Jobs list** | <img src="docs/screenshots/05-job-detail.jpg" width="230"><br>**Job detail** | <img src="docs/screenshots/06-job-checklist.jpg" width="230"><br>**Materials, tools and checklist** |
| <img src="docs/screenshots/07-job-signoff.jpg" width="230"><br>**Photos and signature sign-off** | <img src="docs/screenshots/08-settings-notifications.jpg" width="230"><br>**Notification preferences** | <img src="docs/screenshots/09-settings-quiet-hours.jpg" width="230"><br>**Quiet hours** |
## Architecture Decision Records

See [`/adr`](./adr) for the reasoning behind key choices: kit snapshot immutability, the notification ID scheme, Realtime reload strategy, Supabase free tier as the entire backend, release signing discipline, API key restriction, and pinned dependencies.

## Competency mapping

See [`COMPETENCY_MAP.md`](./COMPETENCY_MAP.md) for how this build maps to cloud and IT competencies.

## Rights and permission

Auto Tech Support has given written permission for this app to be presented publicly as a portfolio piece, including use of the company name. All data shown is seeded test data. No customer information, vehicle identifiers, or business figures appear in this repository or its linked media. The only name shown is the owner's, used with permission.


## Client feedback

> "Before the app I kept everything in my head and on WhatsApp. When too many clients called in one day, jobs slipped through and I would forget to get back to people. Now every job is logged the moment it comes in, nothing gets lost, and I can see exactly what still needs attention. It has changed how we run the business."

Jaques Scholtz, Owner, Auto Tech Support, Johannesburg
