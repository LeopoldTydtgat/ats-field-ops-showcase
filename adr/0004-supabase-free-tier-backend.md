# ADR 0004: Supabase free tier with RLS as the entire backend

**Status:** accepted.

## Context

The client needed a working system at zero running cost. The user base is exactly two invited accounts.

## Decision

Supabase free tier provides Auth (email OTP, signups disabled, invite-only), Postgres with Row Level Security on every table, and Realtime. No custom server. Anonymous role has no access. A GitHub Actions workflow pings the database daily so the free project never pauses.

## Consequences

- Zero monthly cost, no server to patch or monitor.
- Security is enforced at the database layer, not in app code.
- The free-tier pause behaviour is a real operational constraint, handled with a documented keepalive rather than ignored.
- If the team ever grows, the same schema and policies carry to a paid tier unchanged.
