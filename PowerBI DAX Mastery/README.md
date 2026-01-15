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




