# PowerBI DAX Mastery

This directory contains a complete Power BI DAX mastery portfolio showcasing practical implementations, reference material, and analytical models developed using Microsoft Power BI.

## Files Available

This folder contains **three key files**:

- **DAX Mastery (PDF)**  
  Download this PDF to access the complete documentation of DAX concepts, formulas, patterns, and explanations. It serves as a consolidated reference covering calculated columns, measures, evaluation context, filtering, iterators, time intelligence, and advanced DAX techniques.

- **DAX Mastery – AdventureDB**  
  Power BI report built using the AdventureDB dataset, demonstrating end-to-end sales, product, customer, and time intelligence analysis.

- **DAX Mastery – EMP Sales**  
  Power BI report focused on organizational hierarchy and employee sales analysis using advanced DAX patterns.

## Source Data

The datasets used in this project are located in:

Data-Analysis-Report-and-Dashboard/Source data/PowerBi DAX Source/


This source folder contains **two datasets**:
- **AdventureDB (XLSX)**
- **EMP Sales Dataset**

## Purpose

The purpose of this folder is to provide a structured, real-world demonstration of DAX mastery, combining documented theory with applied Power BI models. The content is intended for learning, reference, and portfolio evaluation.

### Intro

In this Power BI project, I managed the full cycle of data modeling and reporting by building relationships between fact and dimension tables, creating calculated columns, and developing advanced measures using DAX. I implemented time intelligence functions such as year-to-date, month-over-month, and rolling averages, while leveraging CALCULATE, FILTER, and SUMX to enable dynamic insights. I designed KPIs for sales, profit margin, and customer retention, optimized performance with variables and query tuning, and validated results through cross-checks. To make the analysis accessible, I built interactive dashboards with slicers, drill-throughs, and bookmarks, and documented all DAX formulas alongside screenshots of the dashboards to ensure clarity, scalability, and ease of future maintenance.
---

<img width="413" height="497" alt="image" src="https://github.com/user-attachments/assets/98876a38-664b-472a-9399-006c72487e8d" />

<img width="902" height="667" alt="image" src="https://github.com/user-attachments/assets/652d922d-d931-4432-8190-80088af2b05f" />

### Calculated Column: 

```DAX
Profit (CC) = Sales[Sales Amount] - Sales[Total Product Cost]
```

``` DAX
Profit Margin (CC) = Sales[Profit (CC)] / Sales[Sales Amount]
```

<img width="828" height="725" alt="image" src="https://github.com/user-attachments/assets/6ebc95d2-1238-4b2b-b201-7bca4d807ae1" />

## Date Table
<img width="975" height="413" alt="image" src="https://github.com/user-attachments/assets/937ac2e1-a84c-49cd-b161-8691e66a858b" />
---
<img width="828" height="725" alt="image" src="https://github.com/user-attachments/assets/9d2e1832-c218-409e-88c1-380c73c08ad6" />
---

## When to use Calculated Column (CC):
<p align="center">
<img width="975" height="197" alt="image" src="https://github.com/user-attachments/assets/1d106eb7-3c65-413b-a166-3744e54f68f5" />
<img width="594" height="455" alt="image" src="https://github.com/user-attachments/assets/f57305e4-cbc3-4623-81ac-3effb4e7f992" />
<p>
  
## Calculated Columns vs Calculated Measures

| Calculated Column | Calculated Measure |
|-------------------|--------------------|
| Slice or filter values | Calculate percentages |
| Categorize texts/numbers | Calculate ratios |
| Expressions strictly bound to current row | Complex aggregations |
| Consume memory | Consume CPU |
| Calculated at refresh time | Calculated on the fly |
| Data can be seen in the Data tab | Not visible in Data tab (only in visuals) |


## DIVIDE() 
```DAX
Total Cost (CM) = SUM(Sales[Total Product Cost])
```
```DAX
Mark UP (CM) = DIVIDE([Profit (CM)],[Total Cost (CM)],0)
```

<img width="705" height="598" alt="image" src="https://github.com/user-attachments/assets/6a52c48e-2563-4d54-8249-02e512dbcd35" />

### COUNT(), COUNTROWS, DISTINCTCOUNT:
```DAX
Total No of Product (CM) = COUNT('Product'[ProductKey])
Total No. of Sales (CM) = COUNTROWS(Sales)
Total No of Product Sold (CM) = DISTINCTCOUNT(Sales[ProductKey])
```
<img width="258" height="156" alt="image" src="https://github.com/user-attachments/assets/02d8d5dd-78b4-417e-8d1c-5e21b8b96596" /> <img width="416" height="170" alt="image" src="https://github.com/user-attachments/assets/8f44e2db-0047-4108-8592-c61f9e2faf95" /> <img width="645" height="181" alt="image" src="https://github.com/user-attachments/assets/6db4ccb5-1580-4f84-bc13-1662e4afa3a9" />


## Min, Max and Average
```DAX
Min Unit Price (CM) = MIN(Sales[Unit Price])
Average Unit Price (CM) = AVERAGE(Sales[Unit Price])
Max Unit Price (CM) = MAX(Sales[Unit Price])
```
<img width="552" height="159" alt="image" src="https://github.com/user-attachments/assets/07b974d5-ba0b-4ff6-8688-5f1980e61a03" />

### COUNTBLANKS
```DAX
Total Reseller (CM) = COUNT(Reseller[ResellerKey])
Reseller without Postal Code (CM) = COUNTBLANK(Reseller[Postal Code])
```
<img width="542" height="119" alt="image" src="https://github.com/user-attachments/assets/11d12c9a-7263-4342-b1fd-910f8c66bb4d" />
<p align = "center"> <img width="922" height="437" alt="image" src="https://github.com/user-attachments/assets/8abc9af8-7211-4853-97aa-98bdaace7522" /></p>
---

## 📄 Row Context

- **What it is:**  
  Row context means that when DAX evaluates an expression, it looks at one row at a time.

- **Where it happens:**  
  - In calculated columns → each row is evaluated separately.  
  - In iterators (like `FILTER()`, `SUMX()`, `AVERAGEX()`, `ADDCOLUMNS()`) → the function goes row by row through a table, creating a row context for each row.  

- **Important to know:**  
  - Row context does not automatically follow relationships between tables.  
  - Row context does not create a filter context by itself.  
  - To turn row context into filter context, you need special functions (like `CALCULATE`).  

- **Measures vs. Row Context:**  
  - Calculated columns and iterators have row context.  
  - Regular measures do not have row context because they work on entire columns/tables, not individual rows.  
  - If you want row-by-row evaluation inside a measure, you must use an iterator (like `SUMX`).  

✅ **In short:**  
Row context = *“DAX is looking at one row at a time.”*  
It exists in calculated columns and iterators, but not in regular measures unless you use an iterator.

---

## 📄 Filter Context

- **What it is:**  
  Filter context means the set of filters applied to your data model when DAX evaluates an expression.  
  It defines which rows of data are visible at the time of calculation.

- **Where it comes from (initial filter context):**  
  ✔ Slicers on a report  
  ✔ Fields in visuals (e.g., rows and columns in a Matrix)  
  ✔ Page or report filters  
  ✔ Other visuals that cross-filter  

- **How it behaves:**  
  - Filters automatically follow relationships in the data model (from the “one” side to the “many” side).  
  - You can modify or replace filter context using the `CALCULATE()` function, which changes the filters before evaluating the expression.  

✅ **In short:**  
Filter context = *“Which rows are included in the calculation.”*  
It comes from slicers, visuals, and filters, and can be changed with `CALCULATE()`.

---
## Initial or incoming filter context
<img width="448" height="381" alt="image" src="https://github.com/user-attachments/assets/2920ddaf-8387-496c-8c56-dd978eef2a74" /><img width="491" height="367" alt="image" src="https://github.com/user-attachments/assets/26344c4b-0b77-4318-8017-5217e7e4d442" />

**The Unit price discount was applicable for purchases through resellers only**
---

## 📄 Evaluation Context in Functions

Different DAX functions change or use evaluation context in specific ways.  
Here are some common examples:

- **RELATED()** → Expands the current row context to bring in values from another table (like a VLOOKUP).  
- **FILTER()** → Creates a new filter context by selecting only a subset of rows that meet certain conditions.  
- **ALL()** → Removes all filters, so calculations are done on the entire table or column.  
- **ALLEXCEPT()** → Removes all filters except the ones you specify, letting you keep certain filters while ignoring others.  
- **EARLIER() / EARLIEST()** → Used in calculated columns to reference values from an outer row context when working inside nested row evaluations (like looping through rows).  

✅ **In short:**  
Evaluation context defines *how DAX interprets row and filter contexts together*.  
Functions like `RELATED`, `FILTER`, `ALL`, and `CALCULATE` allow you to **modify or extend context** to achieve more complex calculations.

---
## RELATED()
```DAX
Current List Price (CC) = RELATED('Product'[List Price])
 ```
<img width="900" height="459" alt="image" src="https://github.com/user-attachments/assets/fa443312-3bb1-4d79-b370-70aa3b9f8ded" />
## Relatedtable()
```DAX
No of Sales (CC) = COUNTROWS(RELATEDTABLE(Sales))
```
<img width="823" height="420" alt="image" src="https://github.com/user-attachments/assets/d10e2143-557e-4f7c-a0df-897b83bdca24" /><img width="678" height="203" alt="image" src="https://github.com/user-attachments/assets/771787e9-2b88-49d4-858b-e4b5d9dd1a49" />

## DISTINCTCOUNT()
```DAX
No of Sales (CC) = COUNTROWS(RELATEDTABLE(Sales))
Last Order Date (CC) = CALCULATE(MAX(Sales[OrderDate]))
No of Product purchased (CC) = DISTINCTCOUNT(Sales[ProductKey])
No of Product purchased CAL (CC) = CALCULATE(DISTINCTCOUNT(Sales[ProductKey]))
```
## VALUE()
```DAX
Testing _CT _ VALUES_ Product (CT) = VALUES('Product') // Whole Table
```
<img width="975" height="132" alt="image" src="https://github.com/user-attachments/assets/e446ae38-b205-4bd1-b81a-c069e0a555ac" />


```DAX
Testing _CT _ VALUES_ Product (CT) = VALUES('Product'[Category])  // Specific Column
```
<img width="831" height="234" alt="image" src="https://github.com/user-attachments/assets/c85424b9-3e62-4ed7-8d10-8fc5a6995e9a" />

### Distinct
```DAX
Testing _CT _ VALUES_ Product (CT) = DISTINCT('Product'[Category])
```
<img width="909" height="298" alt="image" src="https://github.com/user-attachments/assets/f2de86dd-e6f5-4848-b14e-73f853eb6316" />

### ALL()
```DAX
Testing _CT _ VALUES_ Product (CT) = ALL('Product'[Category])
```
<img width="827" height="242" alt="image" src="https://github.com/user-attachments/assets/6169c8dc-b527-421e-ae0f-f1552cdce235" />

### ALL() – 2 Column
```DAX
Testing _CT _ VALUES_ Product -2 COL (CT) = ALL('Product'[Category], 'Product'[Subcategory])
```
<img width="975" height="717" alt="image" src="https://github.com/user-attachments/assets/af45ea5b-f6da-4faa-9cc5-fbca8d1aa223" />

### ERROR
<img width="975" height="104" alt="image" src="https://github.com/user-attachments/assets/95e89c63-22f5-441c-bf49-3c25e40aab5a" />

### SUMMARIZE()
```DAX
Testing _CT _ VALUES_ Product using Summarize(CT) = SUMMARIZE(Sales,'Product'[Category])
```
<img width="975" height="256" alt="image" src="https://github.com/user-attachments/assets/708d8013-5599-4963-8545-839015d052ee" />

```DAX
Testing _CT _ VALUES_ Product using Summarize -2 COL(CT) = SUMMARIZE(Sales,'Product'[Category],'Product'[Subcategory])
```



