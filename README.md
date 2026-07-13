# ISCT

Inventory-and-supply-chain-tracker-with-record-alerts
<br/>
Link - https://1drv.ms/x/c/59e7d09f8555ff0b/IQA5dJTfLW4mTbxFFq9aMraQAXqrAZAJAAdKaUJ0iBSJ0bk?e=1hNWgK
<br/>
<img width="1799" height="633" alt="image" src="https://github.com/user-attachments/assets/ea634c0f-268d-4598-bedf-3b071530c94b" />
<br/>
<img width="1812" height="645" alt="image" src="https://github.com/user-attachments/assets/2af812b9-12f3-43d2-bde0-42f14a324bbc" />



**Supply Chain Performance Report**

*Authors:* Abhirup Bhowmik
*Period covered:* January – December 2024
*Tool:* Microsoft Excel (PivotTables, Slicers, PivotCharts)

**1. Business Problem**

The business tracks daily sales, inventory, and replenishment activity across 50 products, 5 warehouses, 4 regions, and multiple suppliers — but that data sits as 91,250 raw transaction rows with no way to answer basic operational questions at a glance:

- Are we holding too much or too little stock relative to demand?
- Which warehouses/regions are driving sales, and which are underperforming?
- Are supplier lead times causing stock shortages?
- Is the reorder policy (reorder point → order quantity) actually keeping pace with demand, or is it reactive/inconsistent?

Without a consolidated view, these questions require manually filtering and re-filtering a 91k-row spreadsheet every time — too slow for regular operational decisions like adjusting reorder points or flagging underperforming suppliers.

**2. Objective**

Turn the raw transaction log into an interactive dashboard that lets anyone — without touching a formula or filter — see sales, inventory, and replenishment performance by product, warehouse, supplier, and region, and spot problems (overstock, understock, slow suppliers) in seconds.

**3. The Solution: Interactive Dashboard**

Three linked PivotTables drive a dashboard of 6 charts per view (bar, line, doughnut, area, pie), controlled by slicers for *SKU, Warehouse, Supplier,* and *Region*. This directly answers each business question above:

| Business Question | Dashboard Component | How It Answers It |
|---|---|---|
| Is stock aligned with demand? | Inventory vs. Units Sold line/scatter charts | Overlays inventory level against sales over time and as a direct correlation — gaps show over/understock periods |
| Which warehouses/regions need attention? | Bar charts: sales & inventory by Warehouse / Region | Ranks locations side by side instead of scanning raw rows |
| Are suppliers slowing us down? | Supplier lead time vs. inventory/sales scatter charts | Flags suppliers whose lead time correlates with stock dips or missed sales |
| Is the reorder policy working? | Reorder Point vs. Order Quantity / Inventory scatter charts | Shows whether orders are actually triggered near the reorder threshold or lagging behind it |
| "Show me just Warehouse 3's numbers" | Slicers (SKU, Warehouse, Supplier, Region) | One click filters all 6 charts together — no manual re-filtering of raw data |

Because every chart is fed by PivotTables (not hardcoded numbers), the dashboard stays accurate as new daily data is appended — it's a living tool, not a one-time snapshot.

*Three dashboard iterations* (Dashboard, Dashboard_D, Dashboard-d) were built in parallel so different layouts/filter combinations could be compared before settling on the version that communicates the clearest.

**4. Key Findings (Full-Year Totals)**

- *Total units sold:* 30,730
- *Total inventory held (sum across period):* 764,143
- *Total reorder point volume:* 120,099
- *Total order quantity:* 29,900
- *Sales are seasonal:* peak Jan–Apr (~3,550–3,670 units/month), steep decline through Aug–Sep (as low as 1,260/month) — a signal that reorder points set for peak season may over-stock in the back half of the year.
- *Regional demand is fairly even:* South (8,054), North (7,893), West (7,700), East (7,083) — no single region dominates, so replenishment planning can largely be standardized rather than region-specific.

**5. Methodology**

*Data source:* supply_chain_dataset1-selected- sheet — 91,250 raw daily records, kept untouched as the source of truth.

*Step-by-step process:*

1. *Load the raw data* into the workbook without modification, preserving an audit trail back to the original export.
2. *Scope the working dataset.* To make a full, checkable supply chain view achievable (rather than a shallow pass over 50 products), the analysis narrows to one representative product (SKU_1) across all 5 warehouses. This is the Cleaned Data sheet.
3. *Clean the data:*
   - Standardized inconsistent region labels (west → West) so they don't fragment into duplicate categories in the pivots.
   - Interpolated the one missing inventory value from surrounding days so the inventory trend line isn't broken by a gap.
   - Converted the cleaned range into a structured Excel Table (Table2) so pivots and formulas stay in sync as data grows.
4. *Validate the clean.* Used COUNTA() to confirm the expected row count (1,510) — catching any accidental blank rows before analysis.
5. *Summarize with PivotTables* (Overall Blueprint, Comparison Charts, Sheet9, Sheet10) by month, region, warehouse, and supplier, and sanity-checked totals (e.g. regional sums matching the grand total) before building any chart.
6. *Plan every chart against a business question first.* The Dependencies sheet lists all 23 charts with their axes and purpose (e.g. "Supplier delay vs sales") — ensuring the dashboard was built to answer the questions in Section 1, not charted for its own sake.
7. *Build the dashboard*, wiring KPI cards to the pivots with GETPIVOTDATA() and cross-sheet references so headline numbers stay live rather than being typed in as static figures.

**6. Technical Reference**

| Sheet | Role |
|---|---|
| supply_chain_dataset1-selected- | Raw source data (unmodified) |
| Cleaned Data | Cleaned, scoped dataset (Table2) used for analysis |
| Overall Blueprint | Summary KPI pivots (monthly, regional) |
| Dependencies | Chart plan — axis/type/purpose for all 23 charts |
| Comparison Charts | Supporting pivots by warehouse, supplier, region, reorder point |
| Sheet9, Sheet10 | Additional monthly/regional pivot breakdowns feeding the dashboards |
| Dashboard, Dashboard_D, Dashboard-d | Three dashboard iterations (6 charts + slicers each) |

**Functions & features used:**

| Function / Feature | Purpose |
|---|---|
| Excel Table (Table2) | Keeps pivots/formulas synced to the cleaned data range automatically |
| COUNTA() | Validates row counts after cleaning |
| GETPIVOTDATA() | Pulls live summarized values from PivotTables into dashboard KPI cards |
| Cross-sheet references | Feeds pivot totals from Comparison Charts into dashboard cards without duplicating pivots |
| PivotTables | Aggregate data by month/region/warehouse/supplier without manual SUMIFS |
| PivotCharts + Slicers | Drive all dashboard charts from filterable, linked pivot data |

**7. Conclusion**
The dashboard converts a static 91k-row export into a self-service tool that answers the four business questions in Section 1 on demand — without any manual filtering. The clearest operational takeaway is the mismatch between steady reorder point volume and sharply seasonal demand, which is a starting point for revisiting reorder policy going into next year.
