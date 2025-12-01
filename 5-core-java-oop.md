## **1. OOP Overview**

* OOP models real-world entities as **objects** containing **state (fields)** and **behavior (methods)**.
* A **class** is a blueprint / template. It does **not** take memory.
* An **object** is an instance created using `new`, and **that** takes memory.
* OOP’s goal is to improve **modularity, reusability, readability, testability**, and **maintainability**.

---

## **2. Encapsulation**

* It binds data (variables) and methods into a single unit: **class**.
* Sensitive data is hidden using **private** access modifier.
* Controlled access is provided through **public getters and setters**.
* Encapsulation supports **data hiding**, security, and maintainability.

---

## **3. Abstraction**

* Hides complex implementation and exposes only the essential behavior to the user.
* Reduces complexity and increases clarity.
* Achieved via:

  * **Abstract Classes**

    * Can have abstract + non-abstract methods
    * Can have constructors
    * Cannot be instantiated
    * Supports partial abstraction
  * **Interfaces**

    * Provide a contract; implementing class must define method behavior
    * Before Java 8 → methods were abstract
    * Java 8 → default + static methods
    * Java 9 → private helper methods
    * Supports **100% abstraction** before Java 8; now used for multiple inheritance

---

## **4. Inheritance**

* Mechanism where a child class acquires properties and behaviors of a parent class.
* Parent = **superclass/base class**, child = **subclass/derived class**.
* Types:

  * Single
  * Multilevel
  * Hierarchical
  * Hybrid (combination of above)
  * Multiple inheritance → **not allowed** for classes, but **achieved with interfaces**.

**Why Java avoids multiple inheritance for classes?**
To avoid **diamond problem** (ambiguous inheritance path).

---

## **5. Polymorphism**

* Means “many forms”.
* Same method name behaves differently based on context.

### **Two types:**

#### ✔ *Compile-time Polymorphism (Overloading)*

* Same method name, different parameters
* Resolved at **compile time**
* Varies by:

  * Number of arguments
  * Type of arguments
  * Order of arguments

#### ✔ *Runtime Polymorphism (Overriding)*

* Subclass provides its own implementation of a method declared in superclass
* Same method signature
* Resolved at **runtime** using **dynamic dispatch / virtual method table**

---

# 📝 **CORE JAVA + OOP — Final Revision Concise Notes **

### **What is OOP?**

Object-Oriented Programming models real-world entities as **objects** containing:

* **State:** variables
* **Behavior:** methods

A **class** is a blueprint; memory is allocated only when an **object** is created.

### **Why OOP?**

* Reusability
* Modularity
* Maintainability
* Extensibility
* Better code structure

---

### **1. Encapsulation**

* Binding data + behavior inside a class
* Hiding data using `private`
* Exposing access with getters/setters
* Provides security and controlled access

---

### **2. Abstraction**

* Showing essential features; hiding implementation
* Reduces complexity
* Achieved using:

  * **Abstract classes** → partial abstraction, can have both abstract and concrete methods
  * **Interfaces** → provide contract; can have abstract, default, static, and private methods

---

### **3. Inheritance**

* Mechanism to acquire properties/behaviors from another class
* Types: single, multilevel, hierarchical, hybrid
* **Multiple inheritance** not supported for classes → avoids diamond problem
* Can be done via **interfaces**

---

### **4. Polymorphism**

**Compile-Time (Overloading)**

* Same method name, different parameters
* Decided at compile time

**Runtime (Overriding)**

* Subclass overrides superclass method
* Same signature
* Decided at runtime (dynamic dispatch)
