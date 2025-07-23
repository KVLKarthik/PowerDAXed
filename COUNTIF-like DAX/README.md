# 🔢 COUNTIF in Power BI (DAX Patterns)

## 🧠 Overview
This guide demonstrates how to replicate **COUNTIF functionality** in Power BI using `COUNTROWS`, `FILTER`, and `RELATEDTABLE`. These measures help in counting rows based on various conditions like date, product, or channel.


📊 Use Cases
Track transactions for each product or channel.

Identify duplicate entries by date.

Create channel-specific sales counts.

📂 Files
CountIF.pbix — Power BI file with all COUNTIF-style measures.

README.md — This documentation.



---

## 🧮 DAX Measures
2. Duplicated Date Count
Counts how many times the current date appears in Sales.
### **1. Total Transaction Count**
Counts all transactions in the `Sales` table.
```DAX
TransactionCount =
COUNTROWS(Sales)


DuplicatedDateCount =
VAR CurrentRowDate = Sales[Date]
RETURN
COUNTROWS(
    FILTER(
        ALL(Sales),
        Sales[Date] = CurrentRowDate
    )
)

3. Count for Same Product & Channel
Counts all rows where both Product ID and Channel match the current row.

DAX
Copy
Edit
CountForSamePro&Channel =
COUNTROWS(
    FILTER(
        ALL(Sales),
        Sales[Product ID] = EARLIER(Sales[Product ID]) &&
        Sales[Channel] = EARLIER(Sales[Channel])
    )
)
4. Count of Product Sold in Channel = Affiliate
Counts the number of sales for the Affiliate channel.

DAX
Copy
Edit
Count_Affiliate =
COUNTROWS(
    FILTER(
        RELATEDTABLE(Sales),
        Sales[Channel] = "Affiliate"
    )
)
5. Count of Each Product Sold
Counts all sales for the current product.

DAX
Copy
Edit
CountOfProductSold =
COUNTROWS(RELATEDTABLE(Sales))
