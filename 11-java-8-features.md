#  **Java 8 —  Notes (Complete & Crisp)**

---

# ⭐ 1. **Why Java 8? (Most asked intro)**

Java 8 introduced **functional programming** into Java.

### Key goals:

* Write **cleaner, shorter code**
* Better performance using **streams + lazy evaluation**
* Support **parallel processing**
* Strengthen **API design** using functional interfaces

---

# 🔥 2. **Functional Interfaces**

A **functional interface** has **exactly ONE abstract method**.

Examples:

* `Runnable`
* `Callable`
* `Comparator`
* `Supplier`
* `Consumer`
* `Function`

Custom functional interface:

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}
```

---

# 🔥 3. **Lambda Expressions**

Used to implement functional interfaces.

### Syntax:

```java
(parameters) -> { body }
```

Example:

```java
Runnable r = () -> System.out.println("Running");
```

Why useful?

* Reduces boilerplate
* Makes code more readable
* Used heavily in Streams API

---

# 🔥 4. **Method References**

Shortcut for calling an existing method.

Types:

1. `Class::staticMethod`
2. `object::instanceMethod`
3. `Class::instanceMethod`
4. `Class::new` (constructor reference)

Example:

```java
List<String> list = Arrays.asList("a","b");
list.forEach(System.out::println);
```

---

# 🌊 5. **Streams API**

The MOST common Java 8 interview topic.

Stream = **pipeline** of operations:

* Source
* Intermediate operations
* Terminal operation

### ✔ Key features:

* Lazy evaluation
* Functional style
* Supports parallel streams
* Does **not** modify original collection

---

## 🧱 5.1 Stream Pipeline Structure

```java
list.stream()
    .filter(x -> x > 10)       // intermediate
    .map(x -> x * 2)           // intermediate
    .collect(Collectors.toList());  // terminal
```

---

## 🧩 5.2 Intermediate Operations (don’t produce final result)

| Operation       | Purpose                |
| --------------- | ---------------------- |
| filter()        | Keep matching elements |
| map()           | Transform              |
| flatMap()       | Flatten nested lists   |
| sorted()        | Sorting                |
| distinct()      | Remove duplicates      |
| limit(), skip() | Pagination             |

<details><summary><h1>flatMap() example</h1></summary>

  ```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FlatMapExample {
    public static void main(String[] args) {
        List<List<String>> listOfLists = Arrays.asList(
                Arrays.asList("Apple", "Banana"),
                Arrays.asList("Orange", "Grapes"),
                Arrays.asList("Mango", "Pineapple")
        );

        // Using flatMap to flatten the list of lists
        List<String> flatList = listOfLists.stream()
                .flatMap(List::stream) // Flatten each inner list into a single stream
                .collect(Collectors.toList());

        System.out.println(flatList);
    }
}
```

**Output:**

```
[Apple, Banana, Orange, Grapes, Mango, Pineapple]
```

 **Explanation:**

* `listOfLists.stream()` creates a stream of lists.
* `flatMap(List::stream)` converts each inner list into a stream and flattens them into a single stream.
* `collect(Collectors.toList())` collects the flattened elements into a single list.

</details>

---

## 🏁 5.3 Terminal Operations

| Operation              | Purpose                    |
| ---------------------- | -------------------------- |
| collect()              | Convert to list/set/map    |
| forEach()              | Iterate                    |
| reduce()               | Aggregate to single result |
| count()                | Count elements             |
| anyMatch(), allMatch() | Predicate checks           |
| findFirst(), findAny() | Returns Optional           |

---

## 🧠 5.4 Common Stream Interview Questions

### ✔ Count names starting with “A”

```java
names.stream()
     .filter(n -> n.startsWith("A"))
     .count();
```

### ✔ Convert list of objects → list of one field

```java
employees.stream()
         .map(Employee::getName)
         .toList();
```

### ✔ Group by a field

```java
employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));
```

---

# ✔ 6. **Collectors API**

Used for collecting the result of streams.

Most common:

* `Collectors.toList()`
* `Collectors.toSet()`
* `Collectors.toMap()`
* `Collectors.joining(", ")`
* `Collectors.groupingBy()`
* `Collectors.partitioningBy()`
* `Collectors.summingInt()`
* `Collectors.averagingDouble()`

Example: group by department and average salary

```java
.collect(Collectors.groupingBy(
    Employee::getDept,
    Collectors.averagingInt(Employee::getSalary)
));
```

---

# ⭐ 7. **Optional (To avoid NullPointerException)**

Used to handle possibly-null values safely.

### Creating Optional:

```java
Optional<String> opt = Optional.ofNullable(name);
```

### Common methods:

| Method                 | Meaning                            |
| ---------------------- | ---------------------------------- |
| isPresent()            | Check value exists                 |
| orElse(default)        | Return default value               |
| orElseGet(supplier)    | Lazy default                       |
| orElseThrow(exception) | Throw custom exception             |
| map()                  | Transform value                    |
| flatMap()              | Used when mapping returns Optional |

Example:

```java
String name = opt.orElse("Unknown");
```

---

# 🔥 8. **Default & Static Methods in Interfaces**

### Why introduced?

To **evolve interfaces** without breaking existing implementations.

### Default method

```java
interface A {
    default void show() {
        System.out.println("default");
    }
}
```

### Static method

```java
interface A {
    static void util() {
        System.out.println("utility");
    }
}
```

---

# ⚡ 9. **Parallel Streams**

Used for multi-threaded stream execution.

```java
list.parallelStream()
    .map(x -> x * 2)
    .forEach(System.out::println);
```

### Caveats:

* Not good for small data sets
* Not good when operations are not thread-safe
* Works best on **CPU-heavy, large data**

---

# 🧪 10. **Key Differences Interviewers Ask**

### **Stream vs List**

| List               | Stream               |
| ------------------ | -------------------- |
| Stores data        | Doesn't store data   |
| Can modify         | Cannot modify source |
| Eager              | Lazy                 |
| External iteration | Internal iteration   |

---

### **Lambda vs Anonymous Class**

| Lambda                         | Anonymous Class     |
| ------------------------------ | ------------------- |
| Only for functional interfaces | Any interface/class |
| Short                          | Verbose             |
| Better performance             | Slower              |

---

# 🎯 Final Java 8 Summary (Quick Revision)

* Java 8 introduced **functional programming**
* **Functional interfaces** form the core
* **Lambda expressions** reduce boilerplate
* **Streams** enable clean, lazy, functional data processing
* **Optional** reduces NPE
* **Default/static methods** upgraded interfaces
* **Method references** simplify lambda expressions
* **Parallel streams** support multi-threading
