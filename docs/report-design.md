# Report design

## Information hierarchy

1. **Enterprise condition:** inventory, service, capital, and capacity KPIs.
2. **Network imbalance:** where one location has surplus while another has shortage.
3. **Risk type:** surplus, shortage, aging, inactivity, or capacity.
4. **Persistence and source:** future horizon, make/buy, vendor, or operational route.
5. **Actionable grain:** product × warehouse.

## Page strategy

### Inventory Health Overview

Provides the balanced scorecard: total commitment, in-stock/shipable rates, turns, weeks of supply, safety-stock position, and exposure deltas.

### Network Imbalance

Compares location-level surplus and shortage to reveal transfer opportunities and concentrated hotspots.

### Surplus

Segments over-target inventory by risk bucket, lifecycle stage, aging band, warehouse, and product. Value and quantity stay paired.

### Shortage

Separates current and future shortage, make/buy/other source, lead time, vendor concentration, and outage persistence.

### Item–Warehouse Detail

Preserves the accountable operating grain for validation and follow-up.

## Interaction contract

- Shared slicers use governed Calendar, Product, Warehouse, and Vendor dimensions.
- Current/future and value/quantity selectors do not create new relationship paths.
- KPI status colors follow documented thresholds and include text labels.
- Drill-through retains only intended product-location context.
- Narrative insights must reconcile to the numeric measures visible on the page.
