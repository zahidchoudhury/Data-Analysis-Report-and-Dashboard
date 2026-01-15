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

<img width="975" height="531" alt="image" src="https://github.com/user-attachments/assets/300718f8-5802-4344-8ceb-d2f70cb4766d" />

## SUMMARIZE() using measure or expression for GroupBy

```DAX
Testing _CT _ VALUES_ Product using Summarize -using Measures(CT) = 
SUMMARIZE(
 Sales,
'Product'[Category],
'Product'[Subcategory],
"Sales",SUM(Sales[Sales Amount]),
"Total Cost", SUM(Sales[Total Product Cost])
)
```

<img width="933" height="838" alt="image" src="https://github.com/user-attachments/assets/06863842-6584-4fc0-b4a7-5d4a2fb822ce" />

### SUMMARIZE() to get data for all categories:
```DAX
Testing _CT _ VALUES_ Product using Summarize -all category(CT) = 
SUMMARIZE(
 'Product',
'Product'[Category],
'Product'[Subcategory]
)
```
<img width="852" height="872" alt="image" src="https://github.com/user-attachments/assets/c567f3a2-ba14-4ed4-adee-97c252d59b15" />

```DAX
Total Sales Amount (CM) = SUM(Sales[Sales Amount])
 ```

```DAX
Testing _CT _ VALUES_ Product using Summarize -all category(CT) = 
SUMMARIZE(
 'Product',
'Product'[Category],
'Product'[Subcategory],
"SALES", [Total Sales Amount (CM)]
)
```

<img width="880" height="852" alt="image" src="https://github.com/user-attachments/assets/50ff0f37-7993-447a-8a22-baab23f4f768" />

### ALLEXCEPT

```DAX
Testing _CT _ VALUES_ Product using ALLEXCEPT = ALLEXCEPT('Product', 'Product'[ProductKey])
```

<img width="975" height="601" alt="image" src="https://github.com/user-attachments/assets/df20c6ca-9f39-4fd0-86c1-4bc9fac29e0d" />

### FILTER()
```DAX
Testing_CT_Product using Fiter (CT) = FILTER('Product', 'Product'[Category] = "Accessories")
```

<img width="975" height="588" alt="image" src="https://github.com/user-attachments/assets/1ebb4ab2-9b95-4d44-935c-cc5a6109f9e9" />


## Multiple Filter:

```DAX
Testing_CT_Product using Fiter (CT) = 
FILTER('Product', 
'Product'[Category] = "Accessories"
&& 'Product'[List Price]>30
)
```


<img width="975" height="581" alt="image" src="https://github.com/user-attachments/assets/3ad94bd3-c71d-4416-b13a-c491978a75cd" />


### Virtual table lineage (CM)

```DAX
Imaginary Table of customer with sales greater than $5000 = 
CALCULATE( COUNTROWS(Customer),
FILTER(Customer,[Total Sales Amount (CM)]>5000)
)
```

<img width="816" height="555" alt="image" src="https://github.com/user-attachments/assets/73193144-e624-4a6f-b30e-2b59ff9adc51" />

### CT

```DAX
Imaginary_Customer_Sales_Above5000 = 
FILTER (
    Customer,
   [Total Sales Amount (CM)] >= 5000
)
```

<img width="975" height="539" alt="image" src="https://github.com/user-attachments/assets/3f0bd3ef-6252-408e-a1e5-f7f550a3ac34" />

### Mixing_TAB_Filter_ALL (CT)

```DAX
Mixing_TAB_Filter_ALL = 
FILTER (
    ALL ( 'Product'[Category],'Product'[Product],'Product'[List Price]),
    'Product'[Category] = "Accessories" &&
    'Product'[List Price] > 30
)
```
<img width="917" height="780" alt="image" src="https://github.com/user-attachments/assets/fcde6d16-4cd9-477d-abf4-9fc7b6cc0b5d" />

```DAX
Mixing_TAB_Summarize_Filter (CT) = 
FILTER(
    SUMMARIZE(
        'Product',
        'Product'[Category],
        'Product'[Subcategory],
        "Sales", [Total Sales Amount (CM)]
    ),
    'Product'[Category]= "Clothing"
    && [Total Sales Amount (CM)]> 250000
        )
```

<img width="667" height="498" alt="image" src="https://github.com/user-attachments/assets/df1fa661-70a1-4bc6-86bd-c55ce74a46f5" />

### CROSS JOIN(tablee1,table2)

```DAX
Testing_Cross_Join (CT) = CROSSJOIN(Customer,'Product')
```

<img width="975" height="327" alt="image" src="https://github.com/user-attachments/assets/3d48e468-1452-4a7b-a4d3-41bea5b3a99c" />

```DAX
Testing_Cross_Join using Values (CT) = CROSSJOIN(VALUES(Customer[City]),VALUES('Product'[Subcategory]))
 ```

<img width="975" height="738" alt="image" src="https://github.com/user-attachments/assets/a4527f2b-2ce3-4955-b081-449d0d2e5321" />

### Summarize, Values, Cross join

```DAX
Testing Cross join, Summarize,Values (CT) =
SUMMARIZE(CROSSJOIN(VALUES(Customer[City]),VALUES('Product'[Subcategory])),
Customer[City],
'Product'[Subcategory],
"Sales", [Total Sales Amount (CM)])
```

<img width="939" height="850" alt="image" src="https://github.com/user-attachments/assets/fa4132ac-c5c9-4475-90ff-875297f81bd9" />

### Testing Table in Measure (CM)

```DAX
Testing Table using Measures = COUNTROWS(Values('Product'))
```

  <img width="292" height="163" alt="image" src="https://github.com/user-attachments/assets/e0b00734-9ef4-4b3f-b50e-9a2d55ae1d4a" /> <img width="317" height="175" alt="image" src="https://github.com/user-attachments/assets/9746a37c-238a-4cd3-9a1e-51786cb9169b" />

```DAX
Testing Table using Measures (CM) = COUNTROWS(Values('Product'[Product]))
```

 <img width="294" height="159" alt="image" src="https://github.com/user-attachments/assets/40b9bc05-a052-4e54-87ef-4f759baf40b0" />
 
```DAX
Testing Table using Measures (CM) = COUNTROWS(Values('Product'[Subcategory]))
```

 <img width="600" height="367" alt="image" src="https://github.com/user-attachments/assets/10adea50-2d1d-4cae-bd80-8edb393e5142" />

```DAX
Testing Table using Measures (CM) = COUNTROWS(ALL('Product'[Subcategory]))
 ```

<img width="472" height="309" alt="image" src="https://github.com/user-attachments/assets/a49c199d-93f7-44ba-b3a1-4c417fbbb663" />

```DAX
Testing Table using Measures (CM) = COUNTROWS(ALL('Product'[Subcategory]))
 ```

<img width="472" height="309" alt="image" src="https://github.com/user-attachments/assets/29c452da-ce2c-40d9-88fd-be656394db39" />

```DAX
Testing Table using Measures (CM) = COUNTROWS(ALL('Product'[Category]))
```

<img width="472" height="309" alt="image" src="https://github.com/user-attachments/assets/54d4b74b-de20-449a-9b75-d62096495c77" />

```DAX
Testing Table using Measures (CM) = COUNTROWS(ALL('Product'[Category]))
 ```

<img width="438" height="288" alt="image" src="https://github.com/user-attachments/assets/4531f664-cf54-4b74-b410-25782d9a2803" />

### VALUES(), DISTINCT(), ALL() and ALLNOBLANKROW()

```DAX
CountRows using VAlUE (CM) = COUNTROWS(VALUES('Product'))

CountRows using DISTINCT (CM) = COUNTROWS(DISTINCT('Product'))

CountRows using ALL (CM) = COUNTROWS(ALL('Product'))

CountRows using ALLNOBLANK (CM) = COUNTROWS(ALLNOBLANKROW('Product'))
```

<img width="975" height="231" alt="image" src="https://github.com/user-attachments/assets/f225aa5a-2b0a-449f-b8dd-6c0ba69571b7" />

### Variables and Comments in DAX:

```DAX
Testing Variables (CM) = 
VAR TotalQuantity = SUM(Sales[Order Quantity])
RETURN
TotalQuantity
```

<img width="530" height="186" alt="image" src="https://github.com/user-attachments/assets/9415616a-feed-411b-ae83-9368d7abd873" />

```DAX
Testing Variables (CM) = 
VAR TotalQuantity = SUM(Sales[Order Quantity])
RETURN
IF(TotalQuantity >1000, TotalQuantity*0.95, TotalQuantity*1.25)
```

<img width="663" height="355" alt="image" src="https://github.com/user-attachments/assets/580239c3-3c6b-4975-a69a-db8c0276b697" /><img width="692" height="523" alt="image" src="https://github.com/user-attachments/assets/f9380cd0-4987-4c67-8f0c-11bcce6befe8" />

```DAX
No of Premium Bikes (CM) = 
VAR PremiumBikeListPrice = 3000
VAR BikeCategoryProduct =
FILTER('Product','Product'[Category]="Bikes")
VAR PremiumBikeCategoryProducts = 
FILTER(BikeCategoryProduct,'Product'[List Price] > PremiumBikeListPrice)
RETURN
COUNTROWS(PremiumBikeCategoryProducts)
```

<img width="808" height="466" alt="image" src="https://github.com/user-attachments/assets/62c267c0-62d6-4135-bcc3-d7917efe12c5" /><img width="833" height="517" alt="image" src="https://github.com/user-attachments/assets/d04681c3-d1f1-45cb-8494-174bfef2fce2" />

### Iterators

```DAX
Discount Amount (CM) = 
SUMX(Sales,Sales[Unit Price Discount Pct] * Sales[Extended Amount])
```

```DAX
Discount Amount Wrong (CM) = 
SUM(Sales[Unit Price Discount Pct]) * SUM(Sales[Extended Amount])
```

<img width="758" height="441" alt="image" src="https://github.com/user-attachments/assets/0e6c3ccb-e5b7-4909-a6ff-490d5a69e6df" />

```DAX
Discount Amount Large Sales (CM) = 
 VAR LargeSalesTable =
    FILTER(Sales,Sales[Order Quantity] >10)
RETURN
    SUMX( LargeSalesTable, 
    Sales[Unit Price Discount Pct] * Sales[Extended Amount])
```

<img width="808" height="422" alt="image" src="https://github.com/user-attachments/assets/89bb0cc4-d1cd-42d3-a78b-c7c05226f9a9" />
```DAX
AVERAGEX() : to find the average delivery days
Average Deivery Date (CM) = 
AVERAGEX(Sales, Sales[DeliveryDate]-Sales[OrderDate])
```


<img width="636" height="302" alt="image" src="https://github.com/user-attachments/assets/2bf38333-335d-4634-9089-9ec6bcbe4179" /> <img width="652" height="353" alt="image" src="https://github.com/user-attachments/assets/5ca452c0-2fc5-4465-bf9e-772d38d95cbf" />

```DAX
Bonus Amount (CM) = 
SUMX (
    Sales,
    IF ( 
        RELATED ( 'Date'[WorkingDays] ) = "WEEKDAY", //Weedend: Friday & Saturday
        Sales[Sales Amount] * 0.01,
        Sales[Sales Amount] * 0.02
    )
)
```

<img width="647" height="467" alt="image" src="https://github.com/user-attachments/assets/cc1dc0b5-9a5b-499d-8980-bac8bad4c2c5" />

## MINX(), MAXX()
```DAX
Minimum Sales Per Customer (CC) = MINX(RELATEDTABLE(Sales),Sales[Sales Amount])
Maximum Sales Per Customer(CC) = MAXX(RELATEDTABLE(Sales),Sales[Sales Amount])
```

<img width="867" height="394" alt="image" src="https://github.com/user-attachments/assets/fe352e22-22c0-47f4-8dae-6592863e4c3e" />

## AVERAGEX()
```DAX
Average SAles Per Product (CM) = AVERAGEX('Product',[Total Sales Amount (CM)])
```
```DAX
Average Sales Per Product without context Transistion (CM) = AVERAGEX('Product',SUM(Sales[Sales Amount]))
```
<img width="536" height="286" alt="image" src="https://github.com/user-attachments/assets/ac46f51b-e2b7-42cb-913a-57a3ea1de2b1" /><img width="931" height="314" alt="image" src="https://github.com/user-attachments/assets/b4d610f1-30b8-48ba-8f1a-7b16ef28aa1f" /><img width="786" height="256" alt="image" src="https://github.com/user-attachments/assets/0391038e-9c0c-4624-85fe-4c2406866a06" />

```DAX
Average Sales (CM) = AVERAGE(Sales[Sales Amount])

No Of Sales (CM) = COUNTROWS(Sales)

```

<img width="975" height="160" alt="image" src="https://github.com/user-attachments/assets/2a31f7b7-d14f-40c8-9d6d-63051025f95b" />

### Advance Filtering in DAX
Calculate:
```DAX
F_SALES In Australia (CM) = CALCULATE([Total Sales Amount (CM)],SalesTerritory[Country]="Australia")
 ```
<img width="789" height="241" alt="image" src="https://github.com/user-attachments/assets/953ff510-3653-4da2-aec6-d55fb6fbf759" />

```DAX
F_Australia Sales % = DIVIDE([F_SALES In Australia (CM)],[Total Sales Amount (CM)],0)
```
<img width="686" height="244" alt="image" src="https://github.com/user-attachments/assets/be29742b-4bb2-4884-a20a-64e8b5b22f26" />

```DAX
F_SALES In Australia 2 (CM) = 
CALCULATE(
    [Total Sales Amount (CM)],
    FILTER(
         ALL(SalesTerritory[Country]),
        SalesTerritory[Country]= "Australia"
    )
)
```

<img width="898" height="502" alt="image" src="https://github.com/user-attachments/assets/f834cf5b-5e2d-4e19-ac69-77002f427ca4" />

### INTERSECT() & KEEPFILTER()
```DAX
F_Sales in AUS KeepFilter (CM) = 
CALCULATE([Total Sales Amount (CM)],
KEEPFILTERS(SalesTerritory[Country] = "Australia"))
```

 <img width="569" height="353" alt="image" src="https://github.com/user-attachments/assets/821c0b03-1f90-470f-b037-582bc1f81f85" />

 
### Multiple Filter 

````DAX
F_Sales in AUS & CAN = 
CALCULATE([Total Sales Amount (CM)],
(SalesTerritory[Country] = "Australia" || SalesTerritory[Country] = "Canada"))
```

<img width="858" height="406" alt="image" src="https://github.com/user-attachments/assets/7e2b8e8f-b478-4e51-a0e2-8668390552ec" />
```DAX
F_Sales in AUS & CAN KeepFIlter (CM) = 
CALCULATE([Total Sales Amount (CM)],
KEEPFILTERS(SalesTerritory[Country] = "Australia" || SalesTerritory[Country] = "Canada"))
```


<img width="933" height="402" alt="image" src="https://github.com/user-attachments/assets/6334394d-db1a-4fb7-a6bf-1b105adfa043" /><img width="975" height="193" alt="image" src="https://github.com/user-attachments/assets/fc52f4a4-68b4-4f82-8c56-fbe03909a030" />

### IN Keyword

```DAX
F_Sales in AUS & CAN & UK(CM) = 
CALCULATE([Total Sales Amount (CM)],
SalesTerritory[Country] IN { "Australia", "Canada", "United Kingdom"}
)
```

<img width="975" height="318" alt="image" src="https://github.com/user-attachments/assets/be036a66-c7c2-4b04-baed-0e7940c5a46d" />

### Using Filter with Calculate

```DAX
I_Sales when Discount > 500 (CM) = 
CALCULATE([Total Sales Amount (CM)],
FILTER(Sales,[Discout Amount (CM)] > 500)
)
```

<img width="606" height="352" alt="image" src="https://github.com/user-attachments/assets/e6b5ee68-a424-4beb-8eaa-df49b4860a1d" />

```DAX
ALL Sales Amount (CM) = CALCULATE([Total Sales Amount (CM)],ALL(SalesTerritory[Country]))
```

<img width="928" height="258" alt="image" src="https://github.com/user-attachments/assets/f125f761-499a-4ecd-9842-59939f7bbb2c" />

```DAX
A_ RM Sales Amount (CM) = CALCULATE([Total Sales Amount (CM)],REMOVEFILTERS(SalesTerritory[Country]))
```
<img width="975" height="222" alt="image" src="https://github.com/user-attachments/assets/f544bfcd-310b-46a6-b35c-5a0fb9dc80c8" />

```DAX
A_ % of Total Sales (CM) = DIVIDE([Total Sales Amount (CM)],[A_ ALL Sales Amount (CM)],0)
```

<img width="975" height="202" alt="image" src="https://github.com/user-attachments/assets/0d271acc-e7f7-40e3-9268-dd8af507dd25" />
### Slider to test ALLSELECTED

<img width="738" height="173" alt="image" src="https://github.com/user-attachments/assets/93e3b10d-77b5-43a3-b22a-92671e2f3120" />

```DAX
_A ALLselected Country Sales (CM)= CALCULATE([Total Sales Amount (CM)], ALLSELECTED(SalesTerritory))

_A % of Total Sales using ALLSELECTED (CM) = 
DIVIDE([Total Sales Amount (CM)],[_A ALLselected Country Sales (CM)],0)
```


<img width="975" height="299" alt="image" src="https://github.com/user-attachments/assets/5d19baa9-55f2-4835-bd1a-079bb215079a" /><img width="975" height="231" alt="image" src="https://github.com/user-attachments/assets/f3a2efd3-c048-44aa-adde-6edd991e1def" />

# Time Intelligence
```DAX
TI_Custom YTD (CM) = 
 CALCULATE(
    SUM(Sales[Sales Amount]),
    'Date'[Date] >= DATE(2018,1,1)
    && 'Date'[Date] <= DATE(2018,5,18)
 )
```



	 

























 









