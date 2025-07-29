## 📊 Allocation Calculations in Power BI

This Power BI project demonstrates how to perform **cost allocations** across categories and time using sales data, price, and external cost inputs. It’s designed as a practical example of DAX-based revenue and cost modeling for analytics dashboards.

---

### 🎯 Objective

To allocate total cost proportionally across categories like **Product**, **Year**, and **Order Quantity**, using calculated ratios based on sales transactions.

---

### 🧠 Core Concepts

* **Dynamic Allocation** using ratio of:

  * Unit Sales (numerator)
  * Total Category Sales (denominator)
* **Context-Aware Calculations** via `ALLEXCEPT()` and `CALCULATE()`
* **Cost Join** from external dimension table
* **Optimization** with `SUMX()` and `DIVIDE()` for better performance

---

### 🔨 Key Metrics (High-Level)

* **TOTAL SALES**
* **NUMERATOR SALES**
* **DENOMINATOR SALES**
* **TOTAL COST**
* **COST ALLOCATED** (Basic and Optimized)
* **COST CONCAT** for grouping Year + Category

📌 *All calculations are defined at the row level using related tables and later aggregated at the category level.*

---

### 🗃️ Model Overview

* `SalesData` → Fact Table (Order-wise details)
* `Products`, `Cost`, `Calendar` → Dimension Tables
* Relationships defined via `ProductKey` and custom `COST CONCAT`

---

### 🚀 Performance & Tools

* **Used**: Power BI Desktop
* **Performance Analyzer** used to compare DAX alternatives
* **Focus**: Efficient model design, minimal DAX redundancy


CREDIT https://www.youtube.com/watch?v=x2fIFC9lUZo&list=PLr7RyN24TvNYzETX26HxTzzLr2qMH-iT9&index=16
