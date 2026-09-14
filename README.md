# Consumer Complaints and Operational Risk Analytics

An independent Power BI portfolio project using public CFPB consumer complaints data. The dashboard uses an Amex-themed presentation; it is not an internal American Express system or evidence of employment with the company.

## Latest dashboard

![Power BI dashboard showing Midwest credit-reporting complaints](screenshots/2026-09-13-143932.png)

[Download the updated Power BI workbook](Enterprise_Operational_Risk_Dashboard.pbix) · [Open the full-size screenshot](screenshots/2026-09-13-143932.png) · [DAX definitions](docs/dax-measures.md) · [Screenshot history](screenshots/README.md)

Updated September 14, 2026 with the saved September 13 workbook and screenshot. The screenshot filters **Credit reporting, credit repair services, or other personal consumer reports** to the **Midwest** region.

| Metric in this filtered view | Value |
|---|---:|
| Complaints | 804 |
| Untimely responses | 42 |
| Untimely response rate | 5.22% |
| Complaints closed with monetary relief | 30 |

The three counts above were independently reconciled against the saved model; 42 / 804 rounds to 5.22%. These are filtered results, not totals for the full dataset.

## Business question and findings

Where are complaints concentrated, how often are responses untimely, and which issue categories warrant further investigation?

The complete dataset contains **62,516 unique complaints across nine product categories**, including **2,403 untimely responses**. Within 2,736 debt-collection complaints, attempts to collect debt not owed (1,351) and written notification about debt (487) together account for **67.18%**. This concentration provides a starting point for document and process review; it does not establish root causes or quantify savings from a proposed fix.

## Data preparation and modeling

- Loaded public complaint CSV data with Power Query, promoted headers and assigned date, numeric and text types.
- Connected the complaint fact table to calendar and geography dimensions for date and regional analysis.
- Built interactive product and region filters, KPI cards, issue distributions, state-level outcome summaries and submission-channel views.
- Organized measures into folders for core KPIs, time intelligence, formatting and advanced analysis.

## DAX and reporting

The saved model contains 14 measures, including legacy and newer KPI definitions. Calculations cover complaint counts, response timeliness, monetary relief, prior-month totals, month-over-month growth, a 30-day average of daily breach rates, Top 5 issues and conditional alert colors. Functions include `CALCULATE`, `KEEPFILTERS`, `DATEADD`, `AVERAGEX`, `DATESINPERIOD`, `TOPN`, `ALLSELECTED` and `SWITCH`.

See the [complete saved DAX definitions and validation notes](docs/dax-measures.md). Some supporting measures are in the model but are not visible in the screenshot.

## Row-level security configuration

- `Product_Compliance_Lead_Cards`: restricts the complaint table to Credit card, Credit card or prepaid card, and Prepaid card.
- `Regional_Risk_Lead_West`: restricts the complaint table to CA, WA, OR, NV and AZ. This is a five-state scope; it is narrower than the geography table's West region.

These are configured static roles. Power BI View As and service-level security testing have not been documented. The report's region slicer is separate from RLS.

## Review and reproduce

1. Download the PBIX and open it in Power BI Desktop to inspect the saved report and model.
2. For a data refresh, replace the original local CSV path in Power Query with your local copy of the source data. The source schema and types are visible in the query.
3. Select the credit-reporting product and Midwest region to compare against the latest screenshot.
4. Review measure definitions and validate any changes before reusing outputs.

Source: [CFPB Consumer Complaint Database](https://www.consumerfinance.gov/data-research/consumer-complaints/). Complaint records describe reported issues and company responses; they are not verified fraud events or transaction-level loss records. “SLA breach” in the report means the source field `Timely response?` is No. Color thresholds are project assumptions, not legal or regulatory benchmarks.

## Earlier versions

[Earlier web dashboard](https://sehaj64.github.io/amex-operational-risk-dashboard/) · [Earlier PDF report views](pdf_reports/) · [Original screenshot gallery](screenshots/README.md)

The web dashboard and PDFs are earlier presentation versions. They do not reproduce the updated PBIX model, RLS or latest filter state. Refer to the latest screenshot and PBIX for current portfolio evidence.
