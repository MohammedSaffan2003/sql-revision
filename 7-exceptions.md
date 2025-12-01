#  **Exception Handling — Explanation**

### **What are exceptions?**

Exceptions are **abnormal events** that disrupt the normal flow of a program.
They usually occur due to invalid user input, resource unavailability, or logic issues.

Java handles exceptions using a **robust exception-handling mechanism** to prevent program crashes and allow graceful recovery.

---

## **Types of Exceptions**

### **1. Checked Exceptions (Compile-time)**

* Verified by the compiler.
* Must be handled using **try–catch** or declared using **throws**.
* Examples:

  * `IOException`
  * `SQLException`
  * `ClassNotFoundException`

**Why they exist?**
Because the programmer *must* anticipate these conditions (e.g., missing files, network issues).

---

### **2. Unchecked Exceptions (Runtime)**

* Occur during program execution.
* Extend `RuntimeException`.
* Typically caused by programming mistakes.
* Examples:

  * `ArithmeticException`
  * `NullPointerException`
  * `ArrayIndexOutOfBoundsException`

**Why they exist?**
Because many logic errors cannot be detected at compile time.

---

## **Exception Handling Keywords**

### **try–catch**

* Code that may throw an exception goes inside `try`.
* `catch` handles specific exceptions.
* Multiple catch blocks allowed (order: **most specific → most general**).

### **throw**

* Used to **manually throw** an exception.
* Example:
  `throw new IllegalArgumentException("Invalid age");`

### **throws**

* Declares that a method **may throw** an exception.
* Used for *checked* exceptions.

### **finally**

* Executes **always** (exception or not).
* Used for cleanup: closing DB, files, connections.

---

## **Exception Propagation**

If a method does not catch an exception, it is **passed up the call stack** until some method catches it.
Unchecked exceptions propagate automatically; checked ones require `throws`.

---

#  **final vs finally vs finalize (Interview Favorite)**

### **final**

* Keyword
* Used for:

  * final variable → constant
  * final method → cannot be overridden
  * final class → cannot be inherited

### **finally**

* Block
* Executes regardless of an exception
* Used for cleanup

### **finalize (deprecated)**

* Method in `Object` class
* Called by GC *before* object removal
* Not reliable, deprecated in Java 9; removed in Java 18

**One-line interview answer:**
*"final is a keyword, finally is a block, finalize was a cleanup method for GC but is deprecated."*

---
### **If both catch and finally blocks have a return statement, which one executes?**

* If a `return` exists in **try** or **catch**, the **finally block still executes before the method actually returns**.
* If there’s also a `return` inside **finally**, **finally’s return overrides** any previous return from try/catch.

**one-liner:**  *"finally always executes, and if it has a return statement, it overrides the return from try/catch."*

---

# 📝 **Java Exception Handling — Revision Notes**

### **1. What are Exceptions?**

* Abnormal events disrupting normal program flow.
* Usually caused by: invalid input, resource issues, logic errors.
* Java provides **try-catch-finally** mechanism to handle them gracefully.

---

### **2. Types of Exceptions**

| Type      | Checked / Unchecked | When Occurs        | Examples                                                                  |
| --------- | ------------------- | ------------------ | ------------------------------------------------------------------------- |
| Checked   | Compile-time        | Anticipated errors | IOException, SQLException, ClassNotFoundException                         |
| Unchecked | Runtime             | Programming errors | ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException |

---

### **3. Keywords**

**try–catch**

* Place code that may throw exception inside `try`.
* Handle it in `catch`.
* Multiple catch blocks allowed: **specific → general**.

**throw**

* Manually throw an exception.
* Example: `throw new IllegalArgumentException("Invalid input");`

**throws**

* Declares exceptions a method **may throw**.
* Required for **checked exceptions**.

**finally**

* Executes **always**, exception or not.
* Used for cleanup: DB/file closing.

---

### **4. Exception Propagation**

* If a method does not catch an exception, it **propagates up the call stack**.
* Checked exceptions require `throws`; unchecked propagate automatically.

---

### **5. final vs finally vs finalize**

| Keyword / Method | Purpose                                                               | Interview Tip |
| ---------------- | --------------------------------------------------------------------- | ------------- |
| `final`          | Variable → constant, Method → cannot override, Class → cannot inherit | Keyword       |
| `finally`        | Block that always executes (even if exception occurs)                 | Cleanup code  |
| `finalize()`     | Called by GC before object removal; deprecated                        | Avoid using   |

---

### **6. Quick Notes / Tips**

* `catch` executes **only if exception occurs**.
* `finally` executes **always**, even if `try` or `catch` has a return.
* If **finally has return**, it **overrides return from try/catch**.

---

### **7. Example (Interview Style)**

```java
public int example() {
    try {
        return 1;
    } catch(Exception e) {
        return 2;
    } finally {
        return 3; // Overrides all previous returns
    }
}
// This method always returns 3
```
