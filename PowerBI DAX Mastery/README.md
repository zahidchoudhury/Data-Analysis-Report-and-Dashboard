# DAX Mastery – Power BI Portfolio

## Overview

This repository contains a comprehensive **DAX Mastery portfolio** designed to demonstrate practical expertise in **data modeling, analytical problem-solving, and advanced DAX development** using Microsoft Power BI.
The project is built as a progressive, real-world reference covering **foundational to advanced DAX patterns** applied across business, technical, and management-level reporting scenarios.

This portfolio is a **work in progress** and will continue to evolve until it covers **every major analytical use case** commonly encountered in enterprise BI environments.

---

## Datasets Used

The analysis is based on two primary datasets:

1. **AdventureDB (XLSX)**
   Used for:

   * Sales analysis
   * Product and customer analytics
   * Time intelligence and performance metrics

2. **EMP-Sales Dataset**
   Used for:

   * Organizational hierarchies
   * Employee reporting structures
   * Path-based hierarchy analysis

All source files are organized under:

```
/Source Data/PowerBI DAX Source
```

---

## Tools & Technologies

* **Microsoft Power BI**
* **DAX (Data Analysis Expressions)**
* Star schema and relational modeling
* Optimized measure design for scalability and performance

---

## Key Skills Demonstrated

This project showcases the ability to:

* Translate **business requirements into analytical models**
* Design **optimized, reusable, and production-ready DAX measures**
* Build **interactive dashboards and reports**
* Apply **advanced filtering, ranking, and time intelligence**
* Analyze data across **multiple dimensions and hierarchies**
* Handle **complex evaluation contexts** effectively

---

## DAX Concepts Covered

### Core DAX Foundations

* Calculated Columns vs. Calculated Measures
* Row Context, Filter Context, and Evaluation Context
* Context transition and performance considerations

### Aggregations & Iterators

* SUM, AVERAGE, MIN, MAX
* SUMX, AVERAGEX, MINX, MAXX
* COUNT, COUNTROWS, DISTINCTCOUNT

### Filtering & Virtual Tables

* FILTER, ALL, ALLEXCEPT, ALLSELECTED
* REMOVEFILTERS, KEEPFILTERS
* VALUES, DISTINCT, ALLNOBLANKROW
* Virtual table lineage and table expressions

### Advanced DAX Patterns

* Variables (VAR / RETURN)
* Conditional logic (IF, SWITCH)
* Text and search functions
* CONCATENATEX and HASONEVALUE
* ISINSCOPE-based dynamic calculations

### Ranking & Analytics

* Static and dynamic ranking using RANKX
* Context-aware rankings across hierarchies
* Threshold-based spike detection

### Time Intelligence

* YTD, MTD, Running Totals
* SAMEPERIODLASTYEAR, DATEADD
* DATESBETWEEN, DATESINPERIOD
* Fiscal year handling
* Moving totals and YoY growth analysis

### Hierarchies & Organizational Analysis

* PATH, PATHITEM, PATHLENGTH
* Dynamic hierarchy browsing
* Depth-aware calculations
* Hierarchical sales aggregation

---

## Reporting Scope

The reports and measures span:

* **Technical analysis**
* **Business performance reporting**
* **Industry-oriented KPIs**
* **Management-level summaries**

Dashboards are designed from **basic exploratory views** to **advanced executive-ready analytics**.

---

## Project Status

🚧 **In Progress**

This repository is actively being expanded to include:

* Additional real-world scenarios
* Performance-optimized DAX patterns
* Industry-specific analytical use cases

---

## Purpose

This portfolio serves as:

* A **learning reference** for advanced DAX
* A **professional showcase** of Power BI expertise
* A **practical demonstration** of analytical thinking and BI solution design


---

A practical, categorized reference of **commonly used and high-impact DAX functions and patterns**, covering fundamentals through advanced analytical scenarios.

---

## Data Modeling Basics

### Calculated Column vs Measure

```DAX
-- Calculated Column (row context)
Profit (CC) = Sales[Sales Amount] - Sales[Total Product Cost]

-- Measure (filter context)
Profit (CM) =
SUM(Sales[Sales Amount]) - SUM(Sales[Total Product Cost])
```

---

## Aggregation Functions

```DAX
SUM(Sales[Sales Amount])
AVERAGE(Sales[Unit Price])
MIN(Sales[Order Quantity])
MAX(Sales[Order Quantity])
```

---

## Counting Functions

```DAX
COUNT(Product[ProductKey])
COUNTROWS(Sales)
DISTINCTCOUNT(Sales[CustomerKey])
COUNTBLANK(Customer[Postal Code])
```

---

## Iterator Functions (Row-by-Row)

```DAX
SUMX(Sales, Sales[Order Quantity] * Sales[Unit Price])

AVERAGEX(
    Sales,
    Sales[DeliveryDate] - Sales[OrderDate]
)
```

---

## Filter Context & CALCULATE

```DAX
CALCULATE(
    [Total Sales Amount],
    SalesTerritory[Country] = "Australia"
)

CALCULATE(
    [Total Sales Amount],
    SalesTerritory[Country] IN {
        "Australia", "Canada", "United Kingdom"
    }
)
```

---

## Filtering Functions

```DAX
FILTER(
    Product,
    Product[Category] = "Accessories"
)

FILTER(
    Product,
    Product[List Price] > 100
)
```

---

## ALL, ALLEXCEPT, REMOVEFILTERS

```DAX
CALCULATE(
    [Total Sales Amount],
    ALL(Product)
)

CALCULATE(
    [Total Sales Amount],
    ALLEXCEPT(Product, Product[Category])
)

CALCULATE(
    [Total Sales Amount],
    REMOVEFILTERS(SalesTerritory[Country])
)
```

---

## VALUES, DISTINCT, ALLSELECTED

```DAX
VALUES(Product[Category])
DISTINCT(Customer[City])

CALCULATE(
    [Total Sales Amount],
    ALLSELECTED(Product)
)
```

---

## Virtual Tables

```DAX
SUMMARIZE(
    Sales,
    Product[Category],
    "Sales", SUM(Sales[Sales Amount])
)

CROSSJOIN(
    VALUES(Customer[City]),
    VALUES(Product[Subcategory])
)
```

---

## Variables (Best Practice)

```DAX
VAR TotalSales = [Total Sales Amount]
VAR TotalCost  = [Total Cost Amount]
RETURN
    TotalSales - TotalCost
```

---

## Conditional Logic

```DAX
IF([Profit] > 0, "Profit", "Loss")

SWITCH(
    TRUE(),
    [Profit] > 100000, "High",
    [Profit] > 50000, "Medium",
    "Low"
)
```

---

## Ranking & Analytics

```DAX
RANKX(
    ALL(Customer),
    [Total Sales Amount]
)

RANKX(
    ALLEXCEPT(Customer, Customer[Country]),
    [Total Sales Amount]
)
```

---

## Time Intelligence (Requires Date Table)

```DAX
TOTALYTD(
    [Total Sales Amount],
    'Date'[Date]
)

SAMEPERIODLASTYEAR('Date'[Date])

DATESINPERIOD(
    'Date'[Date],
    MAX('Date'[Date]),
    -3,
    MONTH
)
```

---

## Running Total Pattern

```DAX
VAR MaxDate = MAX('Date'[Date])
RETURN
CALCULATE(
    [Total Sales Amount],
    FILTER(
        ALL('Date'),
        'Date'[Date] <= MaxDate
    )
)
```

---

## Context Detection

```DAX
HASONEVALUE(Product[Category])
ISINSCOPE(Product[Subcategory])
```

---

## Hierarchies (Parent–Child)

```DAX
PATH(Employees[EmployeeID], Employees[ManagerID])
PATHLENGTH(Employees[HierarchyPath])
PATHITEM(Employees[HierarchyPath], 2)
```

---

## Text Functions

```DAX
CONCATENATE(Customer[FirstName], Customer[LastName])

CONCATENATEX(
    VALUES(Product[Category]),
    Product[Category],
    ", "
)
```

---

## Performance Tips (Quick Reference)

* Prefer **measures over calculated columns**
* Use **VAR** to avoid repeated calculations
* Avoid **FILTER inside iterators** when possible
* Minimize use of **ALL(Table)** on large tables
* Always use a **proper Date table**

---
