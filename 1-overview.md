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

---

# 🔥 TRIGGERS (Interview Points)

### **What is a trigger?**

A database object that automatically executes **before or after** an INSERT, UPDATE, or DELETE operation.

### **Why do we use triggers?**

* Enforce business rules
* Automatically maintain audit logs
* Validate or transform data before saving

### **When NOT to use triggers?**

* When logic becomes too hidden or hard to debug
* When same logic can be done in application layer
* When performance is critical (triggers slow writes)

### **Example you can explain verbally:**

*"When an employee’s salary changes, a trigger can insert a row into a salary_history table to track the change."*

---

# 🔥 ASSERTIONS (Interview Points)

> Note: Assertions are part of SQL standard but **not supported by MySQL**, which uses CHECK constraints instead.

### **What is an assertion?**

A condition that must always be true in the database.

### **Example (SQL standard):**

```sql
CREATE ASSERTION emp_salary_check
CHECK (
    NOT EXISTS (
        SELECT *
        FROM employees
        WHERE salary < 0
    )
);
```

### **Why assertions matter conceptually?**

* They enforce **global integrity rules** across multiple tables.
* They are like **database-level business validation rules**.

### **MySQL equivalent?**

* Use **CHECK constraints**, **triggers**, or application logic.
* Example:

```sql
ALTER TABLE employees 
ADD CONSTRAINT salary_check CHECK (salary >= 0);
```

### **How to answer in an interview:**

*"MySQL doesn't support assertions, so we use CHECK constraints or triggers to enforce cross-table or complex business rules."*
