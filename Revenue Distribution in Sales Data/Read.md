📊 Revenue Distribution in Sales Data
This Power BI file explores how revenue and cost can be analyzed and broken down across different product categories and years.

🔧 Features Included
Sales & Cost Columns
Custom columns using DAX:

TOTAL SALES

TOTAL COST → based on related cost table

COST CONCAT → combines year and category

Normalized Measures

NUMERATOR SALES and DENOMINATOR SALES for ratio-based visuals

Relationship Mapping

Fact table SalesData linked to Cost, Products, and Calendar

📁 File Structure
Tables:

SalesData (fact)

Products, Cost, Calendar (dimensions)

Measures/Columns:
Core metrics include:

DAX
Copy
Edit
COST CONCAT = YEAR(SalesData[OrderDate]) & " | " & RELATED(Products[Category])

TOTAL COST = RELATED(Cost[Cost])
🔍 Purpose
Practice cost-revenue allocation logic

Build slicer-responsive visualizations

Show foundational use of RELATED() and SUMX()

📌 Status
🚧 Work In Progress
