# Metric contracts

These public-safe contracts show required governance. Threshold values and named owners must come from approved operational policy.

## Shared grain and valuation contract

- **Primary grain:** product × warehouse × snapshot/future week.
- **Time:** current snapshot and future horizon are explicitly separated.
- **Cost basis/currency:** one approved valuation basis and conversion date per published cohort.
- **Ownership cutoff:** on-order/in-transit eligibility follows declared title/control rules.
- **Unknown attributes:** remain visible in a governed unknown member; they are not silently discarded.

| Metric family | Contract concern | Decision/action |
|---|---|---|
| Total commitment | Components are non-overlapping under ownership/status rules | Understand capital committed across supply states |
| ATP in-stock rate | Eligible active product-locations and positive-ATP rule are explicit | Prioritize service availability |
| Shippable rate | Physical and status eligibility is governed | Separate stock from executable service |
| Turns / DOH / WOS | Numerator/denominator periods and zero-demand policy are declared | Evaluate capital efficiency |
| Safety-stock position | Target source, effective date, and exception rule are controlled | Identify under/over protection |
| Shortage and surplus | Gross quantities/values remain visible and use exclusive classes | Drive expedite/rebalance/defer decisions |
| Persistence class | Window and missing-week handling are explicit | Separate transient from structural risk |
| Capacity utilization | Warehouse class, usable capacity, threshold owner, and hysteresis are declared | Escalate capacity risk without alert flapping |

## Governance lifecycle

Proposal → metric-owner approval → data/semantic implementation → reconciliation → playbook mapping → report acceptance → usage/quality review → versioned change/deprecation.

