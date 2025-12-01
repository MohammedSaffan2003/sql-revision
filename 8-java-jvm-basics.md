#  **Java JVM Basics — Notes**

### **1. What is JVM?**

* **JVM (Java Virtual Machine)** is a **runtime engine** that executes Java bytecode.
* Java is **platform-independent** because JVM abstracts the OS/hardware.
* JVM is part of **JRE** (Java Runtime Environment).

**Key Roles:**

1. Load `.class` files (bytecode)
2. Verify bytecode
3. Execute bytecode
4. Manage memory and garbage collection

---

### **2. JVM Architecture**

1. **Class Loader Subsystem**

   * Loads class files into memory.
   * Types of class loaders:

     * **Bootstrap ClassLoader** – loads core Java classes (`java.*`)
     * **Extension ClassLoader** – loads classes from `lib/ext`
     * **System/Application ClassLoader** – loads project-specific classes

2. **Runtime Data Areas**

   * **Method Area / Permanent Generation / Metaspace**

     * Stores class info, constants, static variables
   * **Heap**

     * Stores objects and arrays
     * Garbage collected
   * **Stack**

     * Each thread has its stack
     * Stores method call frames and local variables
   * **PC Register**

     * Program Counter for current executing instruction
   * **Native Method Stack**

     * For native code execution (C/C++)

3. **Execution Engine**

   * Reads bytecode and executes instructions.
   * Components:

     * **Interpreter** – executes bytecode line by line
     * **JIT (Just-In-Time) Compiler** – compiles bytecode to native code for performance

4. **Native Method Interface (JNI)**

   * Allows Java to interact with native code (C/C++)

5. **Garbage Collector**

   * Automatic memory management
   * Removes objects no longer referenced
   * Common algorithms:

     * Serial GC
     * Parallel GC
     * G1 GC (Garbage-First)

---

### **3. JVM Memory Model (Important for Interviews)**

| Memory Area             | Purpose                   | Notes                 |
| ----------------------- | ------------------------- | --------------------- |
| Heap                    | Objects & Arrays          | GC-managed            |
| Stack                   | Method call frames        | LIFO; thread-specific |
| Method Area / Metaspace | Class info, static fields | Shared across threads |
| PC Register             | Current instruction       | Thread-specific       |
| Native Method Stack     | Native code calls         | Platform-dependent    |

---

### **4. JRE vs JDK vs JVM**

| Component | What it includes                      |
| --------- | ------------------------------------- |
| JVM       | Executes bytecode                     |
| JRE       | JVM + Libraries + Runtime environment |
| JDK       | JRE + Compiler + Development tools    |

---

### **5. Common Interview Questions & Tips**

* **Q1: Difference between JRE, JVM, JDK?** → Memorize table above
* **Q2: What is Metaspace?** → Replaced PermGen since Java 8; stores class metadata
* **Q3: What is JIT?** → Improves performance by compiling bytecode to native code
* **Q4: How JVM handles memory?** → Heap + Stack + GC
* **Q5: Types of GC?** → Serial, Parallel, CMS, G1

---

### **6. Quick Notes for Recall**

* JVM is platform-independent → “Write once, run anywhere”
* JVM is inside JRE
* JIT improves runtime performance
* Garbage collection is automatic; stack and heap have different lifetimes
* Each thread has its own **stack** but shares **heap & method area**
---

```
                        +---------------------+
                        |     Class Loader    |
                        |---------------------|
                        | Loads .class files  |
                        +---------------------+
                                 |
                                 v
                        +---------------------+
                        |     Method Area     |
                        |---------------------|
                        | Class info, static  |
                        | constants, metadata |
                        +---------------------+
                                 |
                 +---------------+----------------+
                 |                                |
                 v                                v
           +-----------+                   +-------------+
           |   Heap    |                   |   Stack     |
           |-----------|                   |-------------|
           | Objects & |                   | Method call |
           |  Arrays   |                   | frames,    |
           | GC-managed|                   | local vars |
           +-----------+                   +-------------+
                 |                                |
                 v                                v
          +-----------------+           +-------------------+
          | Garbage Collector|           | PC Register       |
          |-----------------|           |------------------|
          | Removes unref'd |           | Current instr.   |
          | objects         |           +------------------+
          +-----------------+
                 |
                 v
          +------------------+
          | Execution Engine |
          |------------------|
          | Interpreter      |
          | JIT Compiler     |
          +------------------+
                 |
                 v
          +------------------+
          | Native Method    |
          | Interface (JNI) |
          +------------------+
```

---

 **Notes for using this**

* Explain the **flow**: Class Loader → Method Area → Heap/Stack → Execution Engine
* Mention **thread-specific areas** (Stack, PC Register) vs **shared areas** (Heap, Method Area)
* Highlight **GC role** and **JIT optimization**

Simple JVM architecture diagram

![JVM Architecture – Simple Overview](https://media.geeksforgeeks.org/wp-content/uploads/20190614230114/JVM-Architecture-diagram.jpg)

JVM memory areas diagram (heap, stack, method area, PC register …)

![JVM Memory Areas](https://media.geeksforgeeks.org/wp-content/uploads/20251001122044452955/class_loader.webp)

Detailed internal architecture diagram (class‑loader, runtime areas, execution engine, GC)

![JVM Internal Architecture – Detailed](https://techvidvan.com/tutorials/wp-content/uploads/sites/2/2020/06/JVM-Model.jpg)

![Difference Between JDK, JRE, And JVM](https://techvidvan.com/tutorials/wp-content/uploads/sites/2/2020/06/Difference-Between-JDK-JRE-JVM.jpg)
