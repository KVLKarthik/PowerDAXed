# 📉 Bottom N Analysis (Month & Year Wise)

## 🧠 Overview
This page highlights the **least selling products** by calculating their ranks (ascending order of Total Sales) and displaying:
- **Second least selling product**
- **Three least selling products (names)**
- **Sales values of the three least selling products**

📊 Use Cases
Identify bottom N performers at a month or year level.

Pinpoint products dragging down performance.

Useful for inventory or marketing strategy.

📂 Files
BottomNAnalysis.pbix — Power BI file with these measures.

README.md — Documentation for the DAX logic.

📄 Page Name
Bottom N Analysis (Month-Year Wise)

CREDIT 
https://www.youtube.com/watch?v=XBt4mkYIGyI&list=PLr7RyN24TvNYzETX26HxTzzLr2qMH-iT9&index=12

---

## 🧮 DAX Measures

### **1. Least Selling Product**                                   
```DAX
LeastSellingProduct =
CONCATENATEX(
    FILTER(
        Products,
        RANKX(
            Products,
            [Total Sales],
            ,
            ASC,
            DENSE
        ) = 2
    ),
    Products[Product]
)

3LeastSellingProductsSales =
CONCATENATEX(
    FILTER(
        Products,
        VAR RANKED =
            RANKX(
                Products,
                [Total Sales],
                ,
                ASC,
                DENSE
            )
        RETURN
            RANKED >= 2 && RANKED <= 4
    ),
    FORMAT([Total Sales], 0),
    UNICHAR(10),
    [Total Sales]
)

3LeastSellingProducts =
CONCATENATEX(
    FILTER(
        Products,
        VAR RANKED =
            RANKX(
                Products,
                [Total Sales],
                ,
                ASC,
                DENSE
            )
        RETURN
            RANKED >= 2 && RANKED <= 4
    ),
    Products[Product],
    UNICHAR(10)
)

