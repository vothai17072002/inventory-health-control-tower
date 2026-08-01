# Inventory-health DAX patterns

These examples use synthetic objects and demonstrate calculation structure only. They are not production measures. Each pattern depends on the eligibility and accounting rules in the [metric contracts](../docs/metric-contracts.md).

## Commitment value without stage double counting

`On Hand`, `In Transit`, and `On Order` must be mutually exclusive lifecycle states at the selected as-of timestamp. The Gold layer should resolve ownership transfer, cancellation, receipt, currency, and valuation basis before the values reach this measure.

```dax
Total Inventory Commitment :=
VAR EligibleCommitment =
    CALCULATE(
        SUM(FactInventoryCommitment[CommitmentValueReportingCurrency]),
        KEEPFILTERS(FactInventoryCommitment[IsOwnedCommitment] = TRUE()),
        KEEPFILTERS(FactInventoryCommitment[IsCurrentStage] = TRUE()),
        KEEPFILTERS(FactInventoryCommitment[IsCancelled] = FALSE())
    )
RETURN
    EligibleCommitment
```

The source fact should enforce one current lifecycle stage per commitment line. Summing three independently prepared values is unsafe unless reconciliation proves that their populations do not overlap.

## Eligible ATP rate

```dax
ATP In-Stock Rate % :=
DIVIDE(
    [Eligible Active Product-Location Count with Positive ATP],
    [Eligible Active Product-Location Count]
)
```

The denominator contract excludes discontinued products, inactive locations, non-stocked combinations, records outside the as-of window, and combinations with unknown ATP. A blank result means no eligible population; it must not be presented as zero performance.

## Closed-snapshot comparison

```dax
Inventory Value Prior Closed Week :=
VAR CurrentClosedWeekEnd = [Latest Closed Inventory Week End]
VAR PriorClosedWeekEnd = CurrentClosedWeekEnd - 7
RETURN
    CALCULATE(
        [Total Inventory Commitment],
        REMOVEFILTERS(DimDate),
        DimDate[Date] = PriorClosedWeekEnd
    )
```

This pattern avoids comparing an incomplete current week with a closed prior week. It assumes a continuous, marked date table and a governed closed-period flag.

## Gross risk before net position

```dax
Gross Risk Exposure :=
[Surplus Exposure Value] + [Shortage Exposure Value]
```

```dax
Directional Net Risk Position :=
[Surplus Exposure Value] - [Shortage Exposure Value]
```

Gross shortage and surplus remain visible beside the directional net position. Netting alone can conceal two large, operationally different risks that happen to offset numerically.

## Capacity thresholds by warehouse class

Thresholds belong in a governed configuration table, not in hard-coded DAX. A recovery threshold below the entry threshold provides hysteresis and prevents status oscillation near a boundary.

```dax
Capacity Risk Status :=
VAR Utilization = [Capacity Utilization %]
VAR CurrentStatus = SELECTEDVALUE(FactCapacitySnapshot[PriorRiskStatus], "Healthy")
VAR WatchEnter = SELECTEDVALUE(DimWarehouseThreshold[WatchEnterPct])
VAR WatchExit = SELECTEDVALUE(DimWarehouseThreshold[WatchExitPct])
VAR CriticalEnter = SELECTEDVALUE(DimWarehouseThreshold[CriticalEnterPct])
VAR CriticalExit = SELECTEDVALUE(DimWarehouseThreshold[CriticalExitPct])
RETURN
    SWITCH(
        TRUE(),
        ISBLANK(Utilization), "No capacity data",
        ISBLANK(WatchEnter) || ISBLANK(CriticalEnter), "Missing threshold",
        CurrentStatus = "Critical" && Utilization >= CriticalExit, "Critical",
        CurrentStatus = "Watch" && Utilization >= WatchExit && Utilization < CriticalEnter, "Watch",
        Utilization >= CriticalEnter, "Critical",
        Utilization >= WatchEnter, "Watch",
        "Healthy"
    )
```

Threshold ownership, effective dates, unit-of-measure compatibility, and warehouse-class coverage are release-blocking contract checks.

## Minimum synthetic edge cases

| Case | Expected behavior |
|---|---|
| Receipt and in-transit record overlap | One lifecycle stage is eligible; reconciliation fails if both remain current |
| ATP denominator is empty | Rate returns blank and the visual shows “No eligible population” |
| Shortage and surplus are both large and equal | Gross risk remains large; directional net position is zero |
| Warehouse has no governed class threshold | Status is “Missing threshold” and publication is blocked |
| Utilization moves just below an entry threshold | Existing Watch/Critical status follows the lower exit threshold, avoiding alert flapping |
| Current week is incomplete | Comparison uses the latest closed snapshot, not the open period |
