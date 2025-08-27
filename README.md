# SuperStore Sales Analytical Dashboard

**A Power BI dashboard that visualizes SuperStore sales performance** — KPIs, trends, regional & category breakdowns, discount vs. profitability analysis, and interactive slicers to explore the data.

---

## Contents
- `SuperStore Sales Analytical Dashboard.pbix` — Power BI report (source PBIX).  
- `sales.pdf` — Exported PDF of the dashboard (snapshot).  
- `README.md` — This file.

---

## Overview / What this dashboard shows
This dashboard consolidates the SuperStore dataset to surface business-critical insights:

- **KPIs:** Total Sales, Total Profit, Total Quantity, Total Orders, Average Discount, Profit Margin %.  
- **Time series:** Sales & Profit trends over time (monthly / yearly).  
- **Category & sub-category analysis:** Sales and profit distribution across Product Category and Sub-category.  
- **Regional breakdown:** Sales and profit by Region and State/City.  
- **Discount impact:** How discounting affects profitability (scatter or combo visual).  
- **Interactivity:** Slicers for Category, Region, Ship Mode and Date to filter visuals.

---

## Key Insights (summary)
1. **Category Performance:** Technology leads in sales; Furniture has high volume but lower margins.  
2. **Regional Performance:** West region contributes the highest revenue; South lags behind.  
3. **Profit vs Discount:** Higher discounts are correlated with lower profit margins in several sub-categories.  
4. **Seasonality:** Sales show recurring peaks — plan inventory and promotions around high-demand months.  
5. **Orders vs Profit:** High order counts do not always translate to high profitability — identify low-margin top-sellers.

---

## Business Value / Recommendations
- Focus marketing and expansion on high-margin categories and high-performing regions.  
- Revisit discount strategies for sub-categories that lose profit with heavy discounts.  
- Use time-series forecasts to plan inventory and seasonal campaigns.  
- Drill into underperforming sub-categories (low margin, high volume) for pricing or product-mix adjustments.

---

## How to open and explore
1. **View (recommended):** Open `SuperStore Sales Analytical Dashboard.pbix` in **Power BI Desktop**.  
2. **If you don't have PBIX:** Open `sales.pdf` to view static snapshots of the dashboard.  
3. **Interact:** Use the slicers (Category, Region, Ship Mode, Date) to filter the entire report and drill into details.  
4. **Edit:** In Power BI Desktop you can edit visuals, measures, themes, or export updated reports to PDF.

---

## Core Measures (DAX) — copy/paste ready
Replace `'TableName'` with your fact table name:
```DAX
Total Sales = SUM('TableName'[Sales])

Total Profit = SUM('TableName'[Profit])

Total Quantity = SUM('TableName'[Quantity])

Total Orders = DISTINCTCOUNT('TableName'[Order ID])

Average Discount = AVERAGE('TableName'[Discount])

Profit Margin % = DIVIDE(SUM('TableName'[Profit]), SUM('TableName'[Sales]), 0)
```

---

## Date table (recommended DAX)
Create a standard Date table for reliable time-intelligence:
```DAX
DateTable =
CALENDAR (DATE(2015,1,1), DATE(2020,12,31))

DateTable[Year] = YEAR(DateTable[Date])
DateTable[MonthNumber] = MONTH(DateTable[Date])
DateTable[MonthName] = FORMAT(DateTable[Date],"MMM")
DateTable[Quarter] = "Q" & FORMAT(DateTable[Date],"Q")
```
Mark `DateTable` as the Date Table and create a one-to-many relationship to your fact table on `Order Date`.

---

## Visuals used (recommended mapping)
- KPI cards — Total Sales, Total Profit, Total Orders, Profit Margin %.  
- Line/Area charts — Sales & Profit trends over time.  
- Clustered bar/column charts — Sales / Profit by Category, Sub-category, Region.  
- Scatter plot — Discount vs Profit (to spot correlation/outliers).  
- Map (filled or bubble) — Sales by state/region (if geographic data available).  
- Slicers — Category, Region, Ship Mode, Date (Between / Relative).

---

## Formatting & Theming
- Format currency fields (Sales, Profit) with Currency format (choose your currency symbol).  
- Format Discount and Profit Margin as Percentage.  
- Use consistent colors for categories via **Format → Data colors** or save a custom theme for consistency across pages.

---

## Tips to reproduce or extend
- Use the DateTable for all time-intelligence functions (SAMEPERIODLASTYEAR, DATEADD, TOTALYTD).  
- Add measures for YoY and MoM growth:
  ```DAX
  Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DateTable[Date]))
  Sales YoY % = DIVIDE([Total Sales] - [Sales LY], [Sales LY], 0)
  ```
- For category color consistency: in each chart, set **Data colors** manually or define a theme JSON and apply via **View → Themes → Browse for themes**.

---

## Limitations & notes
- `sales.pdf` is a static snapshot — interactive filtering is only available in the PBIX file.  
- The start/end dates in the DateTable should match your dataset range; adjust `CALENDAR()` accordingly.  
- Any drill-throughs, bookmarks, or custom visuals included in the PBIX will require Power BI Desktop to interact.

---

## Contact / Author
If you need further help (custom measures, storytelling, or exporting summaries), open an issue in this repository or contact the author.

---

## License
This dashboard and README are provided for internal analysis and learning. Reuse and modification are allowed — attribute the author where possible.

---

*End of README*
