# Testing strategy

## Data tests

- Enforce one record per documented product-location-snapshot grain.
- Reconcile on-hand, in-transit, on-order, ATP, and total commitment components.
- Validate safety-stock and demand-risk eligibility rules.
- Check current snapshots against future-week facts at the boundary week.
- Test missing cost, vendor, lead-time, and capacity attributes.

## Semantic tests

- Verify value and quantity variants under identical filters.
- Validate current, prior, delta, and delta-percent measure families.
- Confirm disconnected selectors do not filter physical tables unexpectedly.
- Test shortage/surplus buckets for mutual exclusivity and completeness.
- Validate make/buy/other shares sum to the expected eligible population.

## UX and accessibility

- Confirm navigation between Overview, Network, Surplus, Shortage, and Detail.
- Validate keyboard order, contrast, alt text, and non-color status labels.
- Keep default views decision-focused and move dense detail to drill paths.
- Profile cards and matrices with realistic filter cardinality.

## Release gate

Publish only after grain, component reconciliation, risk classification, visual interactions, accessibility, performance, and target-environment binding are verified.
