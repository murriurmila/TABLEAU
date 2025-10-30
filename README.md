# Interactive Sales Dashboard in Tableau

## Overview
Interactive Tableau dashboard analyzing superstore sales with:
- Region, Category, Time filters
- YoY Growth using LOD
- Top 10 Customers + "Others" grouping
- Parameter-driven KPI selection

## Data Source
Cleaned sales data from Databricks Delta Lake → exported as `sales_cleaned.csv`

## Key Calculations
```tableau
// YoY Sales Growth
{FIXED [Region]: SUM(IF YEAR([Order Date]) = [Year Parameter] THEN [Sales] END)} 
/ {FIXED [Region]: SUM(IF YEAR([Order Date]) = [Year Parameter] - 1 THEN [Sales] END)} - 1

// Top N + Others
IF RANK(SUM([Sales])) <= [Top N Parameter] THEN [Customer Name] ELSE 'Others' END
