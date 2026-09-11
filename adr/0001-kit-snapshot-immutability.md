# ADR 0001: Kit snapshots are immutable at job-attach time

**Status:** accepted, proven on device.

## Context

Kits are reusable templates of materials and tools. Jobs attach kits. Kits get edited over time as the team refines them.

## Decision

When a kit is attached to a job, the app stores a full JSON snapshot of its materials and tools on the join row. Later edits, renames, or deletion of the kit never change what an existing job shows.

## Consequences

- A completed job is a truthful record of what was actually specified at the time.
- Exports for invoicing stay consistent with what the team took to site.
- Deleting a kit is safe: the foreign key nulls out, the snapshot and name copy remain.
- The trade-off is data duplication, which is negligible at this scale and worth the correctness.
