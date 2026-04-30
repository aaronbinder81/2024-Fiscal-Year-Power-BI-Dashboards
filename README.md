# Finance & Budget Dashboard — Power BI

An interactive, multi-page financial dashboard built in Power BI Desktop using simulated FY2024 corporate data. Designed to demonstrate end-to-end business intelligence skills including data modeling, DAX measure writing, and executive-ready visual design.

---

## Preview

> *Screenshots coming soon — open the `.pbix` file or view the exported PDF below.*

📄 [View Full Dashboard (PDF)](exports/finance_dashboard.pdf)

---

## Dashboard Pages

### Page 1 — Executive Summary
High-level KPIs and trend overview for leadership. Includes budget vs. actual spend trend, department spend distribution, variance by department, and revenue achievement by product line. Filterable by quarter using a button slicer.

### Page 2 — Budget vs. Actuals Deep Dive
Department-level variance analysis with a monthly heatmap, side-by-side clustered bar chart, waterfall chart showing cumulative variance, and a budget utilization trend line.

### Page 3 — Expense Transactions & Payroll
Granular expense analysis including a transaction-level table, monthly spend by category, category breakdown donut chart, and department payroll vs. budget comparison. Filterable by department and approval status.

---

## Dataset

Four CSV files were used to build this dashboard. All data is simulated for portfolio purposes.

| File | Description | Rows |
|---|---|---|
| `budget_vs_actuals.csv` | Monthly budget vs. actual spend by department | 72 |
| `expense_transactions.csv` | Individual transactions with vendor, category, and payment detail | 500 |
| `revenue_vs_target.csv` | Monthly revenue vs. target by product line | 60 |
| `headcount_payroll.csv` | Department headcount and payroll summary | 6 |

---

## Data Model

The four tables are connected via a star schema with a central `DateTable` built in DAX:

```
DateTable[Date] → budget_vs_actuals[Month]
DateTable[Date] → expense_transactions[Date]
budget_vs_actuals[Department] → headcount_payroll[Department]
expense_transactions[Department] → headcount_payroll[Department]
```

---

## DAX Measures

Key measures written for this project:

```dax
Total Budget = SUM(budget_vs_actuals[Budget])
Total Actual Spend = SUM(budget_vs_actuals[Actual])
Total Variance = SUM(budget_vs_actuals[Variance])
Variance % = DIVIDE([Total Variance], [Total Budget], 0)
Budget Utilization % = DIVIDE([Total Actual Spend], [Total Budget], 0)
Total Revenue = SUM(revenue_vs_target[Actual_Revenue])
Revenue Achievement % = DIVIDE([Total Revenue], [Revenue Target], 0)
Approved Expenses = CALCULATE(SUM(expense_transactions[Amount]),
                   expense_transactions[Approved] = "Yes")
Budget Remaining Label =
    VAR diff = [Total Budget] - [Total Actual Spend]
    RETURN
        IF(diff > 0, "▼ $" & FORMAT(diff, "#,0") & " under budget",
                     "▲ $" & FORMAT(ABS(diff), "#,0") & " over budget")
```

---

## Skills Demonstrated

- Data modeling with relationships across multiple tables
- DAX measure creation including DIVIDE, CALCULATE, and VAR/RETURN
- Date intelligence using a custom Calendar table
- Conditional formatting with diverging color scales
- Multi-page dashboard layout and navigation
- Interactive slicers, cross-filtering, and drill-through
- Finance domain knowledge — variance analysis, budget utilization, payroll tracking
- Executive dashboard design principles

---

## How to Open

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free)
2. Clone or download this repository
3. Open `dashboard/finance_dashboard.pbix`
4. The data is embedded — no additional setup required

---

## Project Structure

```
finance-budget-powerbi-dashboard/
├── README.md
├── dashboard/
│   └── finance_dashboard.pbix
├── data/
│   ├── budget_vs_actuals.csv
│   ├── expense_transactions.csv
│   ├── revenue_vs_target.csv
│   └── headcount_payroll.csv
├── exports/
│   ├── finance_dashboard.pdf
│   ├── page1_executive_summary.png
│   ├── page2_budget_actuals.png
│   └── page3_expenses_payroll.png
└── docs/
    └── PowerBI_Finance_Dashboard_Guide.md
```

---

## Author

**Aaron**
Data Science Student · Eastern University
