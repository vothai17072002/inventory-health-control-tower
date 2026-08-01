# Report design

## Information hierarchy

1. **Enterprise condition:** inventory, service, capital, and capacity KPIs.
2. **Network imbalance:** where one location has surplus while another has shortage.
3. **Risk type:** surplus, shortage, aging, inactivity, or capacity.
4. **Persistence and source:** future horizon, make/buy/other, vendor, or route.
5. **Actionable grain:** product × warehouse.

## Page decision contracts

### Inventory Health Overview

Provides total commitment, in-stock/shippable rates, turns, weeks of supply, safety-stock position, and exposure deltas. The exit outcome is a prioritized domain requiring accountable investigation.

### Network Imbalance

Compares location-level surplus and shortage. A transfer is proposed only after route feasibility, lead time, cost, available quantity, receiving capacity, service priority, and ownership are checked.

### Surplus

Segments over-target inventory by risk bucket, lifecycle stage, aging band, warehouse, and product. Value and quantity stay paired; classes map to transfer, defer/cancel supply, disposition review, or escalation playbooks.

### Shortage

Separates current/future shortage, make/buy/other source, lead time, vendor concentration, and persistence. Playbooks include expedite, rebalance, source escalation, or demand-priority review.

### Item–Warehouse Detail

Preserves the accountable operating grain for validation and follow-up.

### Route Checking

Validates movement feasibility by route, lead time, transfer cost, available quantity, receiving capacity, and service priority. The exit outcome is an approved transfer candidate or documented escalation reason.

## Interaction contract

- Shared slicers use governed Calendar, Product, Warehouse, and Vendor dimensions.
- Current/future and value/quantity selectors do not create new relationship paths.
- KPI status colors follow documented thresholds and include text labels.
- Drill-through retains only intended product-location context.
- Narrative insights reconcile to numeric measures visible in the same filter context.

## AI and custom-visual governance

- Ground text only in active filter context and governed measures.
- Suppress output when freshness, reconciliation, minimum-population, confidence, or authorization policy fails.
- Review data transmission, certification, privacy, accessibility, versioning, and fallback behavior.
- Keep a native numeric/visual fallback so the decision flow does not depend on one extension.

## Performance and maintainability budget

- Count active query visuals per page and interaction fan-out.
- Establish P50/P95 targets only from representative telemetry.
- Cap matrix cardinality and use drill paths for long-tail detail.
- Profile DAX/query shape before increasing capacity.
- Assign an owner and deprecation path to custom visuals and navigation patterns.
