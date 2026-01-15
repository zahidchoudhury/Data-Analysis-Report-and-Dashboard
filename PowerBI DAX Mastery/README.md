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

---
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


