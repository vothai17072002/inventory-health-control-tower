# Operating model and failure handling

## Decision rights

| Decision | Accountable role | Consulted roles |
|---|---|---|
| Risk definition, threshold, and playbook | Business metric/process owner | Finance, planning, warehouse operations |
| Snapshot grain and component eligibility | Data domain lead | Source owners, semantic owner |
| Measure behavior and relationships | Semantic owner | Report owner, QA, governance |
| Decision journey and usability | BI product owner | Operational users, accessibility |
| Capacity/performance budget | Platform owner | BI/semantic owners, FinOps |
| Release, incident, rollback | Service owner | Artifact owners and business approver |

## Failure modes

| Failure | Detection | Mitigation | Owner |
|---|---|---|---|
| Components overlap/double count | Reconciliation invariant | Block publication and correct eligibility | Data/metric owner |
| Risk buckets overlap or omit records | Partition contract test | Quarantine affected snapshot | Metric owner |
| Stale/incomplete future plan | Freshness/completeness SLI | Keep last trusted view and label/suppress future insights | Data service owner |
| Slow page or capacity spike | Query/capacity telemetry | Reduce fan-out/cardinality/DAX cost before scaling | BI/platform |
| AI/custom visual unavailable or unsafe | Health, privacy, certification, accessibility checks | Suppress and use native numeric fallback | Product/security |
| Wrong semantic environment | Binding assertion | Block release, rebind, rerun smoke tests | Release owner |

## 10× scale discussion

Measure history growth, product-location cardinality, future-horizon expansion, concurrency, query shape, fallback, and capacity peaks. Levers include aggregate facts, hot/cold retention, narrower Gold/semantic tables, incremental processing, query budgets, calculation-group reuse, capacity isolation, or domain split. Each has freshness, cost, complexity, and user-experience consequences.

## Release and incident flow

Data contract → DQ/reconciliation → semantic golden queries → report functional/accessibility/performance tests → security/custom-visual review → target binding → smoke test → approval. Incident command follows the failed boundary and restores the last trusted publication/binding before root-cause work.

