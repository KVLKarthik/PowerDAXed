# 📈 LY Total Sales (Last Year Partial Comparison)

## 🧠 Overview
This repository contains a DAX measure that calculates **Last Year's Total Sales**, with adjustments for partial-year comparisons.

- When a **single month** is selected, it directly compares sales with the **same month last year** using `SAMEPERIODLASTYEAR`.
- When a **single year** is selected, it dynamically compares the date range to the **corresponding period of the previous year** using `DATESBETWEEN`.

---

## 🧮 DAX Code
```DAX
LY Total Sales =
IF(
    NOT ISBLANK([Total Sales]),
    IF(
        HASONEVALUE('Calendar'[Month]),
        CALCULATE(
            [Total Sales],
            SAMEPERIODLASTYEAR('Calendar'[Date])
        ),
        IF(
            HASONEVALUE('Calendar'[Year]),
            CALCULATE(
                [Total Sales],
                DATESBETWEEN(
                    'Calendar'[Date],
                    EDATE(MIN('Calendar'[Date]), -12),
                    EOMONTH(MAX('Calendar'[Date]), -12)
                )
            )
        )
    )
)

📊 Use Cases
Compare CY vs LY sales at month or year level.

Works with partial periods, ensuring accurate LY comparisons.

Ideal for year-to-date and custom period analysis.

📂 Files
LYTotalSales.pbix — Power BI file with this measure implemented.

README.md — Documentation for the DAX measure.

📚 Source
https://www.youtube.com/watch?v=txUyGVKqs_s&list=PLr7RyN24TvNYzETX26HxTzzLr2qMH-iT9&index=10&t=2s
