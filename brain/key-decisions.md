# Key Decisions

Architectural and strategic decisions that should not be re-litigated without good reason.

---

## [Decision title] — YYYY-MM-DD

**Decision:** [What was decided]

**Why:** [The reason — constraint, tradeoff, insight, or external factor that drove it]

**Alternatives considered:** [What else was on the table]

**Still valid if:** [Conditions that make this decision hold]

---

## Example: Chose Neon over PlanetScale for all new projects — 2024-11-01

**Decision:** Default to Neon (serverless Postgres) for all new projects instead of PlanetScale.

**Why:** PlanetScale dropped their free tier. Neon's branching model fits the PR-based workflow better, and Postgres is more flexible for the data shapes we're building.

**Alternatives considered:** Railway, Supabase (heavier), self-hosted on Fly.

**Still valid if:** Neon's pricing stays competitive and branching keeps working in CI.

---
_Add new decisions at the top. Don't delete old ones — they're the record._
