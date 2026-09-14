# Saved Power BI measures

Extracted from the September 13, 2026 PBIX. These are saved definitions, not a claim that every measure is displayed or independently tested.

## Total Issues

Table: `Real_CFPB_Consumer_Complaints`

```dax
COUNTROWS('Real_CFPB_Consumer_Complaints')
```

## SLA Breaches

Table: `Real_CFPB_Consumer_Complaints`

```dax
CALCULATE(
    COUNTROWS('Real_CFPB_Consumer_Complaints'), 
    'Real_CFPB_Consumer_Complaints'[Timely response?] = "No"
)
```

## SLA Breach Rate %

Table: `Real_CFPB_Consumer_Complaints`

```dax
DIVIDE([SLA Breaches], [Total Issues], 0)
```

## Monetary Remediation Count

Table: `Real_CFPB_Consumer_Complaints`

```dax
CALCULATE(
    COUNTROWS('Real_CFPB_Consumer_Complaints'), 
    'Real_CFPB_Consumer_Complaints'[Company response to consumer] = "Closed with monetary relief"
)
```

## Total_Issues

Table: `_Measures`

```dax
COUNTROWS('Real_CFPB_Consumer_Complaints')
```

## SLA_Breaches

Table: `_Measures`

```dax
CALCULATE(
    [Total Issues],
    'Real_CFPB_Consumer_Complaints'[Timely response?] = "No"
)
```

## SLA Breach_Rate %

Table: `_Measures`

```dax
DIVIDE([SLA Breaches], [Total Issues], 0)
```

## Monetary Remediation_Count

Table: `_Measures`

```dax
CALCULATE(
    [Total Issues],
    KEEPFILTERS('Real_CFPB_Consumer_Complaints'[Company response to consumer] IN {
        "Closed with monetary relief",
        "Closed with relief"
    })
)
```

## Monetary Relief_Rate %

Table: `_Measures`

```dax
DIVIDE([Monetary Remediation Count], [Total Issues], 0)
```

## Issues Prior Month

Table: `_Measures`

```dax
CALCULATE(
    [Total Issues],
    DATEADD('Dim_Calendar'[Date], -1, MONTH)
)
```

## Issues MoM % Growth

Table: `_Measures`

```dax
VAR CurrentM = [Total Issues]
VAR PriorM = [Issues Prior Month]
RETURN
DIVIDE(CurrentM - PriorM, PriorM, 0)
```

## SLA Breach Rate 30D Moving Avg

Table: `_Measures`

```dax
AVERAGEX(
    DATESINPERIOD('Dim_Calendar'[Date], MAX('Dim_Calendar'[Date]), -30, DAY),
    [SLA Breach Rate %]
)
```

## Top 5 Critical Issues

Table: `_Measures`

```dax
CALCULATE(
    [Total Issues],
    KEEPFILTERS(
        TOPN(
            5,
            ALLSELECTED('Real_CFPB_Consumer_Complaints'[Issue]),
            [Total Issues],
            DESC
        )
    )
)
```

## KPI SLA Breach Alert Color

Table: `_Measures`

```dax
VAR BreachRate = [SLA Breach Rate %]
RETURN
SWITCH(
    TRUE(),
    ISBLANK(BreachRate), "#6c757d",      -- Grey
    BreachRate < 0.02, "#198754",        -- Green (Compliance target met: < 2%)
    BreachRate <= 0.05, "#fd7e14",       -- Amber (Warning threshold: 2% - 5%)
    "#dc3545"                            -- Red (Breach escalation: > 5%)
)
```

## Validation notes

The 30-day calculation averages daily breach rates; it is not a pooled 30-day ratio. The alert thresholds are portfolio assumptions, not regulatory requirements. The two monetary-relief count measures use different category definitions, while the rate references the older count. Review that definition before using the rate in a new report. Legacy and newer measure names coexist.
