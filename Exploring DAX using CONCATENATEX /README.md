# 📊 DAX Exploration: Understanding RANKX with CONCATENATEX

## 🚀 Objective

This experiment is designed to deeply understand how `RANKX` works inside Power BI, especially when combined with `ALL()` and iterators like `CONCATENATEX`.

Instead of just using `RANKX`, the goal is to **visualize how ranking is evaluated internally**.

---

## 🧠 Key Concepts Covered

* Filter Context vs Row Context
* Context Transition
* `ALL()` and filter removal
* Iterators (`CONCATENATEX`)
* Dynamic ranking using `RANKX`

---

## 🧪 DAX Measure Used

```DAX
Explore Product Sales =
CONCATENATEX(
    ALL(Products[Product]),
    Products[Product] & " : " &
    [Total Sales] & " - Rank " &
    RANKX(
        ALL(Products[Product]),
        [Total Sales],
        ,
        DESC,
        DENSE
    ),
    UNICHAR(10)
)
```

---

## 🔍 What This Measure Does

This measure:

1. Removes product-level filters using `ALL(Products[Product])`
2. Iterates over all products using `CONCATENATEX`
3. For each product:

   * Calculates total sales
   * Computes rank across all products
4. Concatenates results into a readable multi-line string

---

## ⚙️ Step-by-Step Execution

### 1. ALL(Products[Product])

* Ignores any product filter from visuals
* Returns full list of products

### 2. CONCATENATEX

* Iterates over each product (acts like a loop)
* Evaluates expression row-by-row

### 3. [Total Sales]

* Calculated per product due to context transition

### 4. RANKX

* Ranks each product against all others
* Uses descending order (highest sales = rank 1)
* Uses dense ranking (no gaps)

---

## 📌 Important Behavior

Even though `ALL(Products)` is used:

* Other filters (like Year, Region) still affect results
* Ranking is **global across products but local to other filters**

👉 Example:

* If Year = 2024 → ranking is within 2024
* If Region = South → ranking is within South

---

## 🧯 Why CONCATENATEX?

Normally, you can’t "see" how `RANKX` evaluates internally.

This trick:

* Forces Power BI to output all intermediate results
* Makes debugging and learning easier

---

## ⚠️ Limitations

* Not meant for production dashboards
* Can be slow with large datasets
* Output is text (not structured)

---

## 💡 Key Takeaways

* `RANKX` recalculates ranking per row
* `ALL()` removes only specified filters
* Iterators like `CONCATENATEX` help expose hidden evaluation logic
* Understanding context is more important than memorizing functions

---

## 🔥 Bonus Experiments

Try modifying:

* Replace `ALL(Products[Product])` with `VALUES(Products[Product])`
* Add slicers (Year, Region) and observe ranking changes
* Use `REMOVEFILTERS(Products)` for full global ranking

---

## 🏁 Conclusion

This is not just a DAX measure — it’s a debugging pattern.

If you truly understand this, you’re already ahead of most Power BI developers who treat `RANKX` as a black box.
