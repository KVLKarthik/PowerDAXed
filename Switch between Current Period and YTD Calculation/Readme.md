## 🔁 Switch Between Current Period and YTD in Power BI

This Power BI report enables users to toggle between **Current Period** and **Year-to-Date (YTD)** calculations using a slicer.

### 💡 Key Concepts

* **Calculation Groups**: Created via **Tabular Editor** for flexible measure behavior.
* **DAX-based Switch Logic**: Determines whether to show period-specific or YTD values.
* **Selection Table**: Slicer-driven table with options like `"Current Period"` and `"YTD"`.

### ⚙️ Implementation Highlights

* **Dynamic Measure Logic** via `SWITCH(TRUE(), ...)` for both calculated measures and calculation groups.
* Works with any base measure (e.g., Total Sales, Profit, etc.)
* **Minimal setup**: Just a slicer and selection table required.

CREDIT
https://www.youtube.com/watch?v=x2fIFC9lUZo&list=PLr7RyN24TvNYzETX26HxTzzLr2qMH-iT9&index=16
