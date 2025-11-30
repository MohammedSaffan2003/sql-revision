###  **ROW_NUMBER() Overview**

Think of `ROW_NUMBER()` as a **way to give a unique, sequential number to rows in a partition**.

Basic syntax:

```sql
ROW_NUMBER() OVER (PARTITION BY column1 ORDER BY column2 DESC)
```

* **PARTITION BY** → optional, resets numbering per group
* **ORDER BY** → defines which row gets which number
* **No partition** → numbers the whole result set sequentially

**Common uses in interviews:**

1. Find the top N per group (e.g., highest-paid employee per department)
2. De-duplicate rows keeping the “latest” or “highest”
3. Pagination

---
