# SQL Revision Notes 
## 1. SELECT, WHERE, ORDER BY, LIMIT

**Question:**
Retrieve the **top 3 highest-paid employees** in the IT department, showing only name and salary.

**Reasoning:**

* `WHERE` → filter IT department
* `ORDER BY salary DESC` → highest first
* `LIMIT 3` → take only top 3
* Only select `name` and `salary`

**Correct Query:**

```sql
SELECT name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 3;
```

**Tip:**

* `ORDER BY` must come **before** `LIMIT`, otherwise results may be wrong.

---

## 2. GROUP BY + HAVING + Aggregation

**Question:**
Find **average salary per department** where average > 70000.

**Reasoning:**

* Aggregate functions (AVG, COUNT, SUM) → for groups
* `WHERE` filters rows **before aggregation**
* `HAVING` filters **groups after aggregation**

**Correct Query:**

```sql
SELECT department, AVG(salary) AS avg_sal
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```

**Tip:**

* Cannot use the alias `avg_sal` in HAVING in MySQL
* HAVING can directly use aggregates like `AVG(salary)`

---

## 3. ROW_NUMBER() + PARTITION + Subquery

**Question:**
For each department, find the **highest-paid employee**.

**Reasoning:**

* `PARTITION BY department` → resets numbering per department
* `ORDER BY salary DESC` → highest salary first
* Alias ROW_NUMBER as `rn`
* Filter on `rn = 1` in **outer query** because alias not visible in same SELECT

**Query:**

```sql
SELECT name, department, salary
FROM (
    SELECT name, department, salary,
           ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rn
    FROM employees
) AS t
WHERE rn = 1;
```

**Tip:**

* Subquery needed to filter on `rn`
* `AS t` is mandatory for the derived table in MySQL

---

## 4. JOIN + GROUP BY + HAVING + ORDER BY

**Question:**
Find the **department with highest average salary**.

**Reasoning:**

* Join employees → departments on `department_id`
* Group by department → calculate AVG(salary)
* Sort descending → LIMIT 1 to get the highest

**Query:**

```sql
SELECT d.department_name, AVG(e.salary) AS avg_salary
FROM employees e
JOIN departments d ON e.department_id = d.id
GROUP BY d.department_name
ORDER BY AVG(e.salary) DESC
LIMIT 1;
```

**Tip:**

* Could group by `d.id` if it’s primary key; then selecting `department_name` is safe
* `ORDER BY + LIMIT` is simpler than HAVING with MAX for this case

---

## 5. LIMIT + OFFSET

**Question:**
Fetch 5 rows starting from the 11th row.

**Query Options:**

```sql
LIMIT 5 OFFSET 10;   -- standard syntax
LIMIT 10, 5;         -- MySQL alternate syntax
```

**Tip:**

* OFFSET = number of rows to skip
* LIMIT = number of rows to take

---

## 6. Multi-Join (3 tables)

**Question:**
Get each employee’s name, department_name, role_name.

**Reasoning:**

* Join employees → departments on `department_id`
* Join employees → roles on `role_id`
* Use INNER JOIN because no nulls needed

**Query:**

```sql
SELECT e.name, d.department_name, r.role_name
FROM employees e
JOIN departments d ON e.department_id = d.id
JOIN roles r ON e.role_id = r.id;
```

**Tip:**

* Order of INNER JOINs **does not matter**
* LEFT/RIGHT joins order does matter

---

## ✅ Key Takeaways

* **WHERE** → filters rows **before aggregation**
* **HAVING** → filters **groups**
* **ROW_NUMBER()** → rank rows within partition; needs subquery to filter by alias
* **LIMIT + OFFSET** → pagination
* **INNER JOIN** → combine tables, only matching rows
* **Multi-Join** → extend same logic for 3+ tables
* **GROUP BY primary key** → safe to select other columns from that key
---

# 📝 SQL Quick Reference Cheat Sheet

| Topic                        | Syntax / Example                                         | Notes                                |                            |
| ---------------------------- | -------------------------------------------------------- | ------------------------------------ | -------------------------- |
| **SELECT**                   | `SELECT col1, col2 FROM table;`                          | Choose specific columns              |                            |
| **WHERE**                    | `WHERE col > 100`                                        | Filters rows **before aggregation**  |                            |
| **ORDER BY**                 | `ORDER BY col ASC                                        | DESC`                                | Must come **before LIMIT** |
| **LIMIT + OFFSET**           | `LIMIT 5 OFFSET 10` <br> `LIMIT 10,5`                    | Pagination: skip then take           |                            |
| **GROUP BY**                 | `GROUP BY col1, col2`                                    | Aggregate rows by column(s)          |                            |
| **HAVING**                   | `HAVING AVG(col) > 100`                                  | Filters groups **after aggregation** |                            |
| **JOIN (INNER)**             | `SELECT * FROM a JOIN b ON a.id = b.a_id`                | Only matching rows                   |                            |
| **LEFT/RIGHT JOIN**          | `SELECT * FROM a LEFT JOIN b ON ...`                     | Preserves all rows from left/right   |                            |
| **Multi-Join**               | `JOIN b ON ... JOIN c ON ...`                            | Combine 3+ tables                    |                            |
| **Aggregates**               | `AVG(col), SUM(col), COUNT(*), MAX(col), MIN(col)`       | Use in SELECT or HAVING              |                            |
| **ROW_NUMBER()**             | `ROW_NUMBER() OVER (PARTITION BY col ORDER BY col DESC)` | Needs subquery to filter by alias    |                            |
| **Subquery / Derived table** | `SELECT ... FROM (SELECT ... ) AS t WHERE ...`           | Allows filtering on computed columns |                            |

---

✅ Tip for interviews:

* Always **think about the order of execution**: FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT/OFFSET
* This will help you reason through questions instead of memorizing syntax.
