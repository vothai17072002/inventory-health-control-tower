# Inventory-health DAX patterns

These examples use synthetic objects and demonstrate calculation structure only.

```dax
Total Inventory Commitment :=
[On Hand Value] + [In Transit Value] + [On Order Value]
```

```dax
ATP In-Stock Rate % :=
DIVIDE(
    [Active Product-Location Count with Positive ATP],
    [Eligible Active Product-Location Count]
)
```

```dax
Inventory Value Prior Week :=
CALCULATE(
    [Total Inventory Commitment],
    DATEADD(DimDate[Date], -7, DAY)
)
```

```dax
Net Risk Exposure :=
[Surplus Exposure Value] - [Shortage Exposure Value]
```

```dax
Capacity Risk Status :=
SWITCH(
    TRUE(),
    ISBLANK([Capacity Utilization %]), "No capacity data",
    [Capacity Utilization %] >= 0.95, "Critical",
    [Capacity Utilization %] >= 0.85, "Watch",
    "Healthy"
)
```
