# Finance & Budget Power BI Dashboard Guide

## Overview

This guide walks you through building a **3-page Finance & Budget Dashboard** using the 4 provided CSV files. The finished product is portfolio-ready and showcases key Power BI skills: data modeling, DAX measures, and interactive visuals.

---

## Files Included

| File | Description | Rows |
|---|---|---|
| `budget_vs_actuals.csv` | Monthly budget vs. actual spend by department | 72 |
| `expense_transactions.csv` | Individual expense transactions with vendor/category detail | 500 |
| `revenue_vs_target.csv` | Monthly revenue vs. target by product line | 60 |
| `headcount_payroll.csv` | Department headcount and payroll summary | 6 |

---

## Step 1 — Load the Data

1. Open **Power BI Desktop** → **Home → Get Data → Text/CSV**
2. Load all 4 files
3. In **Power Query Editor**:
   - For `budget_vs_actuals` and `revenue_vs_target`: Change the `Month` column type to **Date** (format `YYYY-MM`)
   - For `expense_transactions`: Change `Date` to **Date** type
   - Click **Close & Apply**

---

## Step 2 — Build the Data Model

Go to **Model view** and create these relationships:

```
budget_vs_actuals[Department]  →  headcount_payroll[Department]  (Many-to-One)
expense_transactions[Department]  →  headcount_payroll[Department]  (Many-to-One)
```

> The `revenue_vs_target` table is standalone (product-level, not department-level).

---

## Step 3 — Create a Date Table (Best Practice)

In **Home → New Table**, paste this DAX:

```dax
DateTable = CALENDAR(DATE(2024,1,1), DATE(2024,12,31))
```

Then add columns:

```dax
Month Name = FORMAT(DateTable[Date], "MMM")
Month Number = MONTH(DateTable[Date])
Quarter = "Q" & QUARTER(DateTable[Date])
Year = YEAR(DateTable[Date])
```

Connect `DateTable[Date]` to both `budget_vs_actuals[Month]` and `expense_transactions[Date]`.

---

## Step 4 — DAX Measures

Create a **Measures** table (Home → Enter Data → name it "Measures", leave blank, load it).

Then add these measures:

```dax
-- Core Budget Measures
Total Budget = SUM(budget_vs_actuals[Budget])
Total Actual Spend = SUM(budget_vs_actuals[Actual])
Total Variance = SUM(budget_vs_actuals[Variance])
Variance % = DIVIDE([Total Variance], [Total Budget], 0)

-- Budget Utilization
Budget Utilization % = DIVIDE([Total Actual Spend], [Total Budget], 0)

-- Revenue Measures
Total Revenue = SUM(revenue_vs_target[Actual_Revenue])
Revenue Target = SUM(revenue_vs_target[Target])
Revenue Achievement % = DIVIDE([Total Revenue], [Revenue Target], 0)

-- Expense Measures
Total Expenses = SUM(expense_transactions[Amount])
Approved Expenses = CALCULATE(SUM(expense_transactions[Amount]),
                    expense_transactions[Approved] = "Yes")

-- Payroll
Total Payroll = SUM(headcount_payroll[Total_Payroll])
Total Headcount = SUM(headcount_payroll[Headcount])
Avg Salary = DIVIDE([Total Payroll], [Total Headcount], 0)
```

---

## Step 5 — Build the 3 Dashboard Pages

---

### Page 1: Executive Summary

**Purpose:** High-level KPIs and trend overview for leadership.

**Visuals to add:**

| Visual | Fields | Notes |
|---|---|---|
| **Card** | `Total Budget` | Format as currency |
| **Card** | `Total Actual Spend` | Format as currency |
| **Card** | `Variance %` | Use conditional formatting: red if negative |
| **Card** | `Revenue Achievement %` | Format as percentage |
| **Line Chart** | X: Month, Y: Budget + Actual Spend | Add a legend |
| **Bar Chart** | X: Department, Y: Variance % | Color bars by positive/negative |
| **Donut Chart** | Category: Department, Values: Total Actual Spend | Shows spend distribution |
| **Slicer** | `DateTable[Quarter]` | Lets viewers filter by quarter |

**Design tips:**
- Use a dark navy (`#1E2D40`) or light gray (`#F4F6F8`) background
- Group cards at the top row, charts below
- Add a title text box: `FY2024 Financial Summary`

---

### Page 2: Budget vs. Actuals Deep Dive

**Purpose:** Department-level budget tracking and variance analysis.

**Visuals to add:**

| Visual | Fields | Notes |
|---|---|---|
| **Clustered Bar Chart** | Y: Department, X: Budget & Actual | Side-by-side comparison |
| **Matrix Table** | Rows: Department, Columns: Month, Values: Variance % | Heatmap-style conditional formatting |
| **Waterfall Chart** | Category: Department, Y: Variance | Shows over/under at a glance |
| **Line Chart** | X: Month, Y: Budget Utilization % | Shows trend over the year |
| **Slicer** | Department | Multi-select enabled |
| **Slicer** | Month | Slider range style |

**Conditional formatting on Matrix:**
- Select the Variance % values → Format → Conditional Formatting → Background Color
- Set red for negative values, green for positive

---

### Page 3: Expense Transactions & Payroll

**Purpose:** Granular expense analysis and workforce cost breakdown.

**Visuals to add:**

| Visual | Fields | Notes |
|---|---|---|
| **Stacked Bar Chart** | X: Month, Y: Total Expenses, Legend: Category | Shows expense composition over time |
| **Treemap** | Category: Category, Values: Total Expenses | Quick visual of biggest spend categories |
| **Table** | Transaction_ID, Date, Vendor, Amount, Category, Approved | Add conditional formatting on Amount |
| **Pie Chart** | Category: Payment_Method, Values: Total Expenses | Payment method breakdown |
| **Bar Chart** | X: Department, Y: Total Payroll + Payroll_Budget | Budget vs actual payroll |
| **Card** | `Total Headcount` | |
| **Slicer** | Department | |
| **Slicer** | Approved (Yes/No) | Highlight unapproved spend |

---

## Step 6 — Polish for Portfolio

### Consistent Branding
- Set a single accent color (e.g., `#2E75B6` blue or `#217346` green) for all charts
- Use the same font throughout (Segoe UI is Power BI's default and looks clean)
- Add your name and "FY2024" to each page footer using a text box

### Interactivity
- Enable **cross-filtering** between visuals (default behavior — just click a bar and others filter)
- Add a **back button** between pages using **Insert → Buttons → Back**
- Add **tooltips**: hover over a bar to show Budget, Actual, and Variance in a tooltip page

### Navigation Panel (Optional but Impressive)
- Insert a narrow rectangle on the left side of each page
- Add **Buttons** (Insert → Buttons → Blank) for each page with icons
- Group them as a nav bar — this makes it look like a real BI app

---

## Skills This Dashboard Demonstrates

- Data modeling with relationships across multiple tables
- DAX measure creation (aggregations, ratios, CALCULATE)
- Date intelligence with a custom Calendar table
- Conditional formatting and color-coded KPIs
- Cross-filtering and interactive slicers
- Multi-page dashboard layout and navigation
- Finance domain knowledge (Budget vs. Actuals, Variance Analysis)

---

## Publishing (Optional)

1. **File → Publish → Publish to Power BI**
2. Sign in with a free Power BI account (powerbi.microsoft.com)
3. Share the link in your portfolio or LinkedIn post

Good luck — this is a strong portfolio piece!
