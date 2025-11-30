# 📝 SQL Theory & Concepts for Interviews

## 1. **ACID Properties**

**What it is:** Ensures reliable transactions in databases.

| Property        | Meaning                                             |
| --------------- | --------------------------------------------------- |
| **Atomicity**   | All parts of a transaction succeed, or none do      |
| **Consistency** | Database remains in a valid state after transaction |
| **Isolation**   | Transactions don’t interfere with each other        |
| **Durability**  | Committed changes are permanent, even after crash   |

**Example answer:**
*"If I transfer money between accounts, atomicity ensures either both debit and credit happen or neither does."*

---

## 2. **Normalization**

**What it is:** Organizing tables to reduce redundancy and improve integrity.

**Forms commonly asked:**

* 1NF: No repeating groups, atomic values
* 2NF: 1NF + all non-key columns depend on the whole primary key
* 3NF: 2NF + no transitive dependency

**Why it matters:**

* Reduces duplication, prevents anomalies, improves consistency.

---

## 3. **Indexes**

**What it is:** A data structure to speed up queries.

**Key points:**

* Types: B-tree (most common), hash, unique, composite
* Trade-off: faster reads, slower writes (inserts/updates)
* Use in `WHERE`, `ORDER BY`, `JOIN` columns

**Example answer:**
*"If I frequently query `employees.department_id`, adding an index there speeds up filtering and joins."*

---

## 4. **Primary Key vs Foreign Key**

| Key         | Purpose                                                                     |
| ----------- | --------------------------------------------------------------------------- |
| Primary Key | Uniquely identifies a row                                                   |
| Foreign Key | References a primary key in another table to maintain referential integrity |

**Tip:** Be ready to explain cascade actions (`ON DELETE CASCADE`).

---

## 5. **Joins & Differences**

* **INNER JOIN:** Only matching rows
* **LEFT JOIN:** All rows from left, match if exists in right
* **RIGHT JOIN:** All rows from right, match if exists in left
* **FULL OUTER JOIN:** All rows from both, matched where possible

**Interview angle:** Often they ask, “What’s the difference between INNER and LEFT JOIN?” — be ready to explain with a simple table example.

---

## 6. **Transactions**

* Begin a transaction: `START TRANSACTION;`
* Commit: `COMMIT;`
* Rollback: `ROLLBACK;`

**Why:** Ensures multiple queries execute safely together.

**Example:** Money transfer, booking systems.

---

## 7. **Views**

* Virtual table created by a query: `CREATE VIEW view_name AS SELECT ...`
* Good for security, abstraction, simplifying complex queries

**Tip:** Explain difference between **view** (virtual) and **table** (physical).

---

## 8. **Stored Procedures & Functions**

* **Stored Procedure:** Pre-written SQL code, can have logic, parameters
* **Function:** Returns a value, can be used in queries

**Interview angle:** Ask for **benefits** — reusability, performance, encapsulation.

---

## 9. **Constraints**

* **NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT**
* Helps enforce **data integrity**

**Tip:** Be ready to explain what happens when constraint is violated.

---

## 10. **Aggregate Functions vs Scalar Functions**

| Function type | Examples                   | Use                     |
| ------------- | -------------------------- | ----------------------- |
| Aggregate     | SUM, AVG, COUNT, MAX, MIN  | Works on groups of rows |
| Scalar        | UPPER(), ROUND(), LENGTH() | Works on single values  |

---

## 11. **Window Functions**

* `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LEAD()`, `LAG()`
* Operate over a **partition of rows**, unlike aggregate functions
* Often used for **ranking, moving averages, cumulative sums**

**Interview tip:** Can explain with example like “top 1 employee per department”.

---

## 12. **Subqueries vs Joins**

* **Subquery:** Nested query, can be scalar or table result
* **Join:** Combines tables side by side
* **Tip:** Interviewers often ask: “When would you use a subquery instead of join?”

Example answer:
*"Filtering using ROW_NUMBER() or EXISTS is easier with subquery."*

---

## 13. **NULLs & Handling**

* `NULL` = unknown or missing value
* Comparison: `NULL = NULL` → FALSE, use `IS NULL`
* Functions: `COALESCE(col, default)` to replace NULLs

**Tip:** Very common verbal question: difference between NULL and empty string.

---

## 14. **Common SQL Interview Questions / Talking Points**

* Difference between DELETE vs TRUNCATE
* Difference between CHAR and VARCHAR
* Difference between clustered vs non-clustered index
* How to optimize queries (indexes, avoiding SELECT *, proper joins)

---

# 📝 SQL Verbal Q&A Cheat Sheet

| Question / Topic                     | Answer / Explanation                                                                                                                                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **ACID properties**                  | Atomicity: all or nothing; Consistency: valid DB state; Isolation: transactions don’t interfere; Durability: committed changes permanent. Example: money transfer.                               |
| **Normalization (1NF, 2NF, 3NF)**    | Organize tables to reduce redundancy: 1NF = atomic values, 2NF = no partial key dependency, 3NF = no transitive dependency.                                                                      |
| **Indexes**                          | Speeds up queries; types: B-tree, hash, unique, composite; trade-off: faster reads, slower writes; use on WHERE, JOIN, ORDER BY columns. Example: index on `department_id` for frequent queries. |
| **Primary vs Foreign Key**           | Primary key: unique row identifier; Foreign key: references primary key to maintain referential integrity. Can define `ON DELETE CASCADE` to auto-delete related rows.                           |
| **INNER vs LEFT JOIN**               | INNER: only matching rows; LEFT: all left rows + matches if any; RIGHT: all right rows + matches if any; FULL OUTER: all rows from both sides. Example: employees + departments.                 |
| **Transactions**                     | Ensure multiple queries succeed/fail together. Commands: `START TRANSACTION`, `COMMIT`, `ROLLBACK`. Example: booking systems, money transfers.                                                   |
| **Views**                            | Virtual table from a query. Good for abstraction, security, simplifying queries. Example: `CREATE VIEW top_employees AS SELECT * FROM employees WHERE salary > 100000;`                          |
| **Stored Procedures vs Functions**   | Procedure: pre-written SQL logic, may not return a value; Function: returns a value, can be used in SELECT. Benefits: reuse, encapsulation, performance.                                         |
| **Constraints**                      | Enforce data integrity: NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT. Example: UNIQUE email prevents duplicates.                                                                   |
| **Aggregate vs Scalar functions**    | Aggregate: operate on groups (SUM, AVG, COUNT); Scalar: operate on single value (UPPER, LENGTH, ROUND).                                                                                          |
| **Window functions**                 | Operate over partitions: `ROW_NUMBER()`, `RANK()`, `LEAD()`, `LAG()`. Example: “Top 1 employee per department” uses ROW_NUMBER().                                                                |
| **Subquery vs Join**                 | Subquery: nested query; Join: combine tables side by side. Example: use subquery with ROW_NUMBER() to filter top records; use join to get department names.                                      |
| **NULLs**                            | Represent missing/unknown values. Use `IS NULL` to check; `COALESCE(col, default)` replaces NULL. Example: `SELECT COALESCE(bonus, 0) FROM employees`.                                           |
| **DELETE vs TRUNCATE**               | DELETE: removes rows, can use WHERE, slower, can rollback; TRUNCATE: removes all rows, faster, cannot rollback in some DBs.                                                                      |
| **CHAR vs VARCHAR**                  | CHAR: fixed-length, pads extra spaces; VARCHAR: variable-length, saves space. Use VARCHAR for variable-length text.                                                                              |
| **Clustered vs Non-Clustered Index** | Clustered: physically orders data in table; Non-clustered: separate structure points to table rows. Clustered: only 1 per table.                                                                 |
| **Query optimization tips**          | Use proper indexes, avoid SELECT *, filter early with WHERE, choose correct join type, avoid unnecessary nested queries.                                                                         |

---

### ✅ Quick Verbal Tips

1. Always **explain reasoning**, not just syntax.
2. Use **examples** from tables you know (employees, departments).
3. Mention **trade-offs** when appropriate (indexes, joins, normalization).
4. For ranking / top-N queries, mention **ROW_NUMBER() + subquery** pattern.
5. For null handling, always explain `IS NULL` vs `=`.
