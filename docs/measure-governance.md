# Measure governance

The observed Inventory Health measure surface is large enough to behave like a public API. Count alone is not value; discoverability, consistency, performance, and safe change are the objectives.

## Layering

1. **Base:** additive quantities and values with no presentation logic.
2. **Business:** governed service, capital, shortage, surplus, and capacity definitions.
3. **Comparative:** prior, delta, delta percent, and current/future variants.
4. **Presentation:** status, color, labels, and dynamic titles.
5. **Narrative/AI grounding:** approved facts formatted for explanation, never a parallel metric definition.

## Rules

- One owner role, description, display folder, format, and test reference per published measure.
- Reuse calculation groups for repeated comparison/display logic only when behavior stays understandable.
- Golden DAX queries cover representative filters and correct-total behavior.
- Usage telemetry informs deprecation; removal uses a versioned window and consumer notice.
- Performance ownership includes Formula/Storage Engine profile and Direct Lake fallback context.
- Report-local measures are limited to non-reusable presentation behavior and remain documented.

## Change review

Review meaning, population, grain, dependencies, performance, RLS impact, consumers, backward compatibility, and rollback before promotion.

