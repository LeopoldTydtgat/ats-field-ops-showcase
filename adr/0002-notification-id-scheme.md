# ADR 0002: Deterministic notification IDs (28-bit FNV-1a base with slot bits)

**Status:** accepted, verified against production code.

## Context

Android local notifications need a stable 32-bit integer ID. Job UUIDs do not fit. Dart's `String.hashCode` is randomly seeded per process, so an ID recomputed after an app or OS restart would not match the pending alarm, and cancels would silently miss. Each job also needs several notification slots: repeat reminders, a group summary, and a daily overdue nag.

## Decision

Hash the job UUID with deterministic FNV-1a (32-bit), mask to a 28-bit base, and give each job a contiguous 8-ID block: `(base << 3) | slot`. The low 3 bits select the slot. Repeats use slots 0 to 6, the group summary sits at slot 7 so it never collides with a repeat, and the daily overdue nag uses a reserved free slot inside the block.

## Consequences

- The same job always maps to the same IDs, across restarts and rebuilds. Cancel and reschedule are exact.
- Cancelling a job sweeps all 8 slots unconditionally, so no orphaned reminders or empty summary groups survive.
- Maximum ID is a 31-bit positive integer, so it never overflows or goes negative.
- Collision odds between two jobs are around one in a million at realistic job counts, an accepted trade-off.
