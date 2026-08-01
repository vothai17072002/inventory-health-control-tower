# Release-blocking test matrix

Production evidence is intentionally omitted. Each blocking test requires attached query output, screenshot, trace, or approval record before release.

| ID | Test | Scenario | Expected invariant | Owner role | Blocking |
|---|---|---|---|---|---|
| IH-DQ-01 | Snapshot grain | Product × warehouse × snapshot/future week | No duplicate eligible records | Data engineering | Yes |
| IH-DQ-02 | Component reconciliation | On hand, in transit, on order | Commitment components reconcile without double count | Data/metric owner | Yes |
| IH-DQ-03 | Temporal boundary | Current snapshot and first future week | No overlap or gap under approved rule | Data owner | Yes |
| IH-KPI-01 | Risk partition | Every eligible product-location | Buckets are mutually exclusive and collectively exhaustive | Metric owner | Yes |
| IH-KPI-02 | Source share | Make/buy/other eligible shortage | Shares total 100% within tolerance | Metric owner | Yes |
| IH-KPI-03 | Value/quantity consistency | Same risk/filter cohort | Cost basis and currency policy reconcile | Finance/data owner | Yes |
| IH-KPI-04 | Gross versus net risk | Large shortage and surplus together | Gross exposures remain visible; net is not sole headline | Product owner | Yes |
| IH-SEM-01 | Selector isolation | Value/quantity/current/future selectors | Helpers create no unintended filter paths | Semantic owner | Yes |
| IH-UX-01 | Playbook path | Surplus, shortage, route scenarios | User reaches an accountable action/exception outcome | BI product owner | Yes |
| IH-AI-01 | Insight grounding | Empty, stale, restricted, low-confidence contexts | Insight suppresses or falls back safely | Product/security | Yes |
| IH-A11Y-01 | Accessibility | Keyboard, screen reader, contrast, non-color status | Meets agreed WCAG-oriented criteria | Report/QA | Yes |
| IH-PERF-01 | Query budget | Representative high-cardinality filter | P95 meets approved page/visual target | BI/platform | Yes |
| IH-SEC-01 | Authorization/export | Allowed and restricted personas | RLS/export behavior matches policy | Security/model owner | Yes |
| IH-DEP-01 | Environment binding | Post-deployment | Report points to intended semantic model | Release owner | Yes |

## Edge-case suite

Synthetic fixtures cover missing cost/currency/vendor/lead time/capacity, zero or negative quantities, late snapshots, no-demand products, warehouse closure, stale future plans, unknown members, and conflicting transfer candidates.

## Performance evidence protocol

Capture Performance Analyzer output, DAX Server Timings, active visual-query count, matrix cardinality, Direct Lake/fallback telemetry, and capacity context. A capacity upgrade is a business trade-off—not a substitute for query and page design review.
