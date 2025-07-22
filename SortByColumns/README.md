# 🔁 Sort By Columns & Date Intelligence in Power BI

## 🧠 Overview

This Power BI file shows how to **control sort order for time-based fields**—Month, Month‑Year, Fiscal Month (Apr–Mar), and Week‑Year—using **supporting DAX sort columns**. It’s built on a `CalendarAxis` date dimension related to `SalesData`.

---

## 📊 What’s Inside

* Proper Month sorting (Jan–Dec) using `MonthNumber`
* Fiscal Month (Apr start) using `FISCALMONTHNUMBER`
* Text Month‑Year (e.g., `Jan_2012`) sortable via `MonthYearSort`
* Week labels sortable via `WeekSort`
* Sample visual: Year + Month + Total Sales to show sort effects

---

## 🧮 DAX Used

**MonthNumber**

```DAX
MonthNumber = MONTH(CalendarAxis[Date])
```

**Fiscal Month Number (Apr = 1)**

```DAX
FISCALMONTHNUMBER = MONTH(EDATE(CalendarAxis[Date], -3))
```

**Month-Year Sort Key**

```DAX
MonthYearSort =
CalendarAxis[YEAR] & UNICHAR(MONTH(CalendarAxis[Date]) + 64)
```

**Week Sort Key**

```DAX
WeekSort =
VAR WeekNum = WEEKNUM(CalendarAxis[Date], 2)
RETURN
CalendarAxis[YEAR] &
SWITCH(
    TRUE(),
    WeekNum <= 26, UNICHAR(WeekNum + 64),
    WeekNum <= 52, "Z"  & UNICHAR(WeekNum + 38),
    "ZZ" & UNICHAR(WeekNum + 12)
)
```

---

## 🔧 How to Use

| Display Column              | Sort By Column    |
| --------------------------- | ----------------- |
| Month                       | MonthNumber       |
| MonthYear (e.g., Jan\_2012) | MonthYearSort     |
| Fiscal Month Name           | FISCALMONTHNUMBER |
| WeekYear text               | WeekSort          |

Select the display column → **Column tools → Sort by column**.

---

## 📂 Files Included

* `SortByColumns.pbix` — Power BI file with date table, DAX, and visuals
* `README.md` — This guide

---

## 📚 Source / Credit

Concept inspired by [Goodly Chandeep tutorial](https://www.youtube.com/watch?v=c0mPvzkf6i0&list=PLr7RyN24TvNYzETX26HxTzzLr2qMH-iT9&index=9).
