# 🔄 Dynamic KPI Switcher (Measure Selector with Slicer)

## 🧠 Overview
This Power BI setup allows you to **switch between KPIs (Total Sales, Commission, Units Sold, Transactions)** using a **single slicer**. Instead of creating multiple visuals for each KPI, you can dynamically toggle between them.

---

## 📊 Scenarios Implemented
1. **Dynamic Filter Table**  
   - A standalone table (`DynamicFilterTable`) is used to provide slicer options:  
     *Total Sales*, *TOTAL COMMISSION*, *Units Sold*, *Transactions*.

2. **KPI Measures**  
   - Core KPIs are calculated:  
     - **Total Sales** – Total revenue from `Sales[Quantity] * Unit Price`.  
     - **Total Commission** – Sum of commission values using product rates.  
     - **Total Units** – Total units sold.  
     - **Transactions** – Count of all sales transactions.

3. **Selection Measure**  
   - Captures the currently selected KPI from the slicer.  
   - Displays a default message (`SELECT A SINGLE VALUE`) if more than one slicer option is selected.

4. **Calculation Measure**  
   - Uses `SWITCH(TRUE(), ...)` logic to return the appropriate KPI value based on the slicer selection.

5. **Visuals**  
   - A **pivot table or matrix** with **Month and Year** as rows/columns.  
   - The **[Calculation]** measure is placed in **Values**, dynamically changing based on slicer selection.

---

## 🛠 Steps to Implement
1. Create `DynamicFilterTable` as a separate table using **DATATABLE**.  
2. Build the **KPI measures** (`Total Sales`, `Total Commission`, `Total Units`, `Transactions`).  
3. Create **Selection** and **Calculation** measures.  
4. Insert a slicer visual and drag **DynamicFilterTable[DynamicFilter]** onto it.  
5. Use **[Calculation]** in the visual values (e.g., matrix by Month and Year).  
6. Done — *BOOM*, a dynamic KPI switcher!

---

## 🧮 DAX Code

### **1. Dynamic Filter Table**
```DAX
DynamicFilterTable =
DATATABLE(
    "DynamicFilter", STRING,
    {
        {"Total Sales"},
        {"TOTAL COMMISSION"},
        {"Units Sold"},
        {"Transactions"}
    }
)

2. KPI Measures
DAX
Copy
Edit
Total Sales =
SUMX(
    Sales,
    Sales[Quantity] * Sales[Unit Price]
)

Total Commission =
SUMX(
    Sales,
    Sales[Quantity] * RELATED(Products[Commission])
)

Total Units =
SUM(Sales[Quantity])

Transactions =
COUNTROWS(Sales)
3. Selection Measure
DAX
Copy
Edit
Selection =
IF(
    COUNTROWS(VALUES(DynamicFilterTable[DynamicFilter])) = 1,
    VALUES(DynamicFilterTable[DynamicFilter]),
    "SELECT A SINGLE VALUE"
)
4. Calculation Measure
DAX
Copy
Edit
Calculation =
SWITCH(
    TRUE(),
    [Selection] = "Total Sales", IF([Total Sales] <> BLANK(), FORMAT([Total Sales], "$0,0.0")),
    [Selection] = "TOTAL COMMISSION", IF([Total Commission] <> BLANK(), FORMAT([Total Commission], "$0,0.0")),
    [Selection] = "Units Sold", [Total Units],
    [Selection] = "Transactions", [Transactions],
    [Selection]
)
