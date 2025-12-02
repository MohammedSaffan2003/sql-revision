# Java + SQL Interview Notes

## Table of Contents
- [SQL](#sql)
- [Core Java + OOP](#core-java--oop)
- [Collections Framework](#collections-framework)
- [Exception Handling](#exception-handling)
- [JVM](#jvm)
- [Garbage Collector](#garbage-collector)
- [Multithreading](#multithreading)
- [Java 8](#java-8)
- [Data Structures & Algorithms (DSA)](#data-structures--algorithms-dsa)

---

## SQL

**1. Basic Queries**
- `SELECT` → choose columns  
- `WHERE` → filter rows  
- `ORDER BY` → sort results  
- `LIMIT` → restrict rows returned  
- `OFFSET` → skip rows  

**Example:**  
```sql
SELECT NAME, SALARY 
FROM EMPLOYEES 
WHERE DEPARTMENT = 'IT' 
ORDER BY SALARY DESC 
LIMIT 3;
````

**2. Aggregations**

* `AVG(), SUM(), COUNT(), MAX(), MIN()`
* `GROUP BY` → group rows
* `HAVING` → filter groups

**Example:**

```sql
SELECT DEPARTMENT, AVG(SALARY) AS AVG_SAL 
FROM EMPLOYEES 
GROUP BY DEPARTMENT 
HAVING AVG(SALARY) > 70000;
```

**3. Joins**

* `INNER JOIN` → only matching rows
* `LEFT/RIGHT JOIN` → preserve one side
* `FULL OUTER JOIN` → preserve both sides

**Example:**

```sql
SELECT E.NAME, D.DEPARTMENT_NAME, R.ROLE_NAME
FROM EMPLOYEES E
JOIN DEPARTMENT D ON E.DEPARTMENT_ID = D.ID
JOIN ROLES R ON E.ROLE_ID = R.ID;
```

**4. Window Functions**

* `ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ...)`
* Often combined with subqueries to find top records per group

**Example:**

```sql
SELECT NAME, DEPARTMENT, SALARY 
FROM (
    SELECT NAME, DEPARTMENT, SALARY,
           ROW_NUMBER() OVER (PARTITION BY DEPARTMENT ORDER BY SALARY DESC) AS RN
    FROM EMPLOYEES
) AS T
WHERE RN = 1;
```

**5. OFFSET & LIMIT**

* `LIMIT 5 OFFSET 10` → returns 5 rows starting from 11th

---

## Core Java + OOP

**1. OOP Overview**

* Class → blueprint (does not occupy memory)
* Object → instance of class (memory allocated at instantiation)
* Key idea: model real-world entities

**2. Encapsulation**

* Combine data + behavior into a single unit (class)
* Use `private` fields, `public` getters/setters
* Protects internal state

**3. Abstraction**

* Hide implementation details, show only necessary features
* Achieved via:

  * **Abstract class:** can have constructor, cannot instantiate
  * **Interface:** contract for implementing classes; Java 8+ supports default, static, private methods

**4. Inheritance**

* Subclass inherits properties + methods from superclass
* Types:

  * Single, Multi-level, Hierarchical, Hybrid
  * Multiple inheritance → via interfaces in Java

**5. Polymorphism**

* Same method name, multiple implementations

  * **Compile-time / Method Overloading** → different arguments
  * **Runtime / Method Overriding** → subclass provides implementation

---

## Collections Framework

**1. Core Interfaces**

* **List:** ordered, allows duplicates

  * ArrayList, LinkedList, Vector, Stack
* **Set:** unique elements

  * HashSet, LinkedHashSet, TreeSet
* **Queue:** FIFO

  * PriorityQueue, Deque, ArrayDeque
* **Map:** key-value pairs

  * HashMap, LinkedHashMap, TreeMap

**2. Key Notes**

* HashMap / HashSet → O(1) average lookup
* TreeMap / TreeSet → sorted, no null keys
* LinkedHashMap / LinkedHashSet → maintain insertion order
* Stack → synchronized, may slow single-threaded programs
* Concurrent collections → thread-safe versions (ConcurrentHashMap, CopyOnWriteArrayList)

---

## Exception Handling

**1. Types**

* **Checked:** compile-time, must handle (FileNotFoundException, SQLException)
* **Unchecked:** runtime, logic errors (NullPointerException, ArrayIndexOutOfBoundsException)

**2. Keywords**

* `try-catch` → handle exceptions
* `throw` → throw an exception explicitly
* `throws` → declare exceptions in method signature
* `finally` → code always executes (cleanup resources)

**3. Difference**

* `final` → variable cannot change, class cannot extend, method cannot override
* `finally` → executes always after try/catch
* `finalize()` → called by garbage collector before object destruction

---

## JVM

* Java Virtual Machine executes bytecode
* Key components:

  * ClassLoader → loads classes
  * Execution Engine → executes instructions
  * Runtime Data Areas → Heap, Stack, Method Area, PC Register, Native Method Stack
* JIT → Just-In-Time compiler improves performance

**Reference diagram:**
![JVM Memory Areas](https://media.geeksforgeeks.org/wp-content/uploads/20251001122044452955/class_loader.webp)

---

## Garbage Collector

* Automatically manages memory
* Removes unreferenced objects
* Types:

  * Serial GC, Parallel GC, CMS, G1 GC
* **Key idea:** avoid manual `delete`; Java uses automatic memory management

---

## Multithreading

* Multiple threads → concurrent execution
* **Thread creation:**

  * `extends Thread`
  * `implements Runnable`
* **Thread lifecycle:** New → Runnable → Running → Waiting → Terminated
* **Key methods:** `start()`, `run()`, `join()`, `sleep()`
* **Synchronization:** avoid race conditions
* **Concurrent collections:** thread-safe usage

---

## Java 8

**1. Functional Programming**

* **Functional interfaces** → one abstract method
* **Lambda expressions** → `(args) -> {body}`
* **Method references** → `Class::method`

**2. Streams API**

* **Intermediate operations:** `filter()`, `map()`, `distinct()`, `sorted()`
* **Terminal operations:** `collect()`, `reduce()`, `count()`, `forEach()`
* **Parallel streams** → multi-threaded processing

**3. Optional**

* Avoid `NullPointerException`
* Methods: `isPresent()`, `orElse()`, `orElseThrow()`, `map()`, `flatMap()`

**4. Default & Static Methods in Interfaces**

* Default → provide implementation
* Static → utility methods

---

## Data Structures & Algorithms (DSA)

**1. Time & Space Complexity**

* Big-O notation: O(1), O(n), O(n²), O(log n), O(n log n)
* Always mention **best, worst, average cases**

**2. Arrays**

* Fixed size, O(1) access
* Patterns: Two pointers, Sliding window, Prefix sum

**3. Strings**

* Immutable → use StringBuilder for mutations
* Common problems: Palindrome, Anagram, Frequency counting

**4. HashMap / HashSet**

* Fast lookup / insert / delete → O(1) avg
* Use cases: counting, duplicates, two-sum, top-K

**5. Sorting**

* Bubble, Insertion, Selection → O(n²)
* MergeSort, QuickSort, HeapSort → O(n log n)

**6. Recursion & Backtracking**

* Base case + recursive step
* Problems: N-Queens, Sudoku, Permutations

**7. Key Patterns**

* Frequency counting → HashMap
* Sorting + two pointers
* Sliding window for subarray/subsequence
* Recursion / DFS / Backtracking
* Heap / PriorityQueue for top K problems
