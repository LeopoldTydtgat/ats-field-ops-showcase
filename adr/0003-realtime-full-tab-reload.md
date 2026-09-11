# ADR 0003: Full tab reload on Realtime events instead of targeted row updates

**Status:** accepted.

## Context

Both phones subscribe to Supabase Realtime so that job and kit changes made by one user appear on the other's phone. The choice was between patching individual rows in local state or reloading the visible tab on any relevant event.

## Decision

Reload the full tab on any job event, debounced via a ticker. Targeted row updates were considered and deliberately deferred.

## Consequences

- Far simpler state management, and no drift between local state and the database.
- At two users and this row count, the reload cost is invisible.
- Targeted updates only become worthwhile at much higher user and row counts. That threshold is documented, so the upgrade path is known rather than accidental.
