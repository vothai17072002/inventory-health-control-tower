# Architecture decisions

## ADR-001 — Separate current snapshot and future-week facts

- **Decision:** Preserve independent temporal grains and compare them through governed measures.
- **Alternative:** Union both into one fact with implicit temporal semantics.
- **Consequence:** More semantic logic, but boundaries and totals remain explainable.
- **Revisit trigger:** A stable common event grain is introduced upstream.

## ADR-002 — Keep gross shortage and surplus primary

- **Decision:** Show gross exposures side by side; net exposure is secondary context.
- **Why:** Netting can make two large opposing risks appear small.
- **Consequence:** Executive pages need disciplined hierarchy to avoid KPI overload.

## ADR-003 — Map risk classification to an operating playbook

- **Decision:** Every governed class has an action, owner role, escalation rule, and closure evidence.
- **Alternative:** Descriptive classification only.
- **Consequence:** More cross-functional governance, but the report becomes an operating product rather than passive BI.

## ADR-004 — Parameterize capacity thresholds

- **Decision:** Thresholds vary by governed warehouse class and use hysteresis where alert flapping is possible.
- **Alternative:** One hard-coded global percentage.
- **Consequence:** Additional master-data ownership is required.

## ADR-005 — AI insights consume metrics; they do not define them

- **Decision:** AI/narrative consumes reconciled measures and fails closed on stale, restricted, or low-confidence contexts.
- **Consequence:** Some contexts show no narrative; numeric decision paths remain available.

## ADR-006 — Environment binding is release-blocking

- **Decision:** Report-to-model binding is a parameterized deployment artifact with a post-deploy assertion.
- **Consequence:** Accidental Dev binding blocks release and triggers rebind/rollback.

