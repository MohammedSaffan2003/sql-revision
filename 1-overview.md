## 🔹 SQL Overview (concise)

### 1. **SELECT**

* Core operation to retrieve data.
* Supports column selection, expressions, aliases.
* Runs *after* FROM but is written first.

### 2. **WHERE**

* Filters rows **before** grouping or aggregation.
* Works with comparisons, AND/OR, LIKE, IN, BETWEEN.

### 3. **ORDER BY**

* Sorts result set (ASC default, DESC optional).
* Can sort by columns or expressions.
* Runs *last* in the logical order.

### 4. **LIMIT / OFFSET**

* Limits number of rows returned.
* `OFFSET` is how many rows to skip.
* MySQL: `LIMIT count OFFSET offset` or `LIMIT offset, count`.

### 5. **Aggregation (COUNT, SUM, AVG, MAX, MIN)**

* Operate on **sets** of rows.
* Without GROUP BY → whole table is one group.

### 6. **GROUP BY**

* Groups rows based on column(s).
* Every selected column must be:

  * In GROUP BY, or
  * Aggregated.

### 7. **HAVING**

* Filters groups **after** aggregation.
* WHERE → filters rows
  HAVING → filters groups

### 8. **JOINS**

* **INNER JOIN** → matching rows only
* **LEFT JOIN** → everything from left + matches
* **RIGHT JOIN** → everything from right + matches
* **FULL JOIN** → both sides + unmatched (not in MySQL, requires workaround)
* **CROSS JOIN** → Cartesian product

Key interview point: What happens when join columns have NULLs.

### 9. **ROW_NUMBER()**

* Window function.
* Assigns unique row index **per partition ordered by something**.
* Often used for:

  * De-duplicating
  * Top-N per group
  * Pagination
