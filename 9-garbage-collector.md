#  **Garbage Collection (GC) in Java —  Notes**

Garbage Collection is **automatic memory management** in JVM.
It **removes objects that are no longer reachable**, preventing memory leaks.

---

## 1️⃣ **Why Garbage Collection?**

* To automatically free heap memory
* To avoid manual memory management (like C/C++)
* To prevent memory leaks & OutOfMemoryError
* To improve performance by recycling unused objects

---

## 2️⃣ **How JVM identifies unused (garbage) objects?**

### ✔ **Reachability Analysis (Root Search Algorithm)**

An object is considered *alive* if reachable from **GC Roots**.

**GC Roots include:**

* Local variables in stack frames
* Static variables
* Active threads
* JNI references
* Class loaders

If an object is not reachable → marked for deletion.

---

## 3️⃣ **Heap Structure (Modern JVM)**

JVM uses a **Generational Heap Model**:

### **1. Young Generation**

* **Eden** (new objects created here)
* **Survivor S0 & S1** (objects that survive minor GC cycles)

GC here is called **Minor GC** (fast).

### **2. Old Generation**

* Long-living objects from Survivor spaces move here.
* GC here is **Major GC** or **Full GC** (slow).

### **3. Metaspace** (since Java 8)

* Stores class metadata (instead of PermGen)

---

## 4️⃣ **Types of Garbage Collectors (Modern JVM)**

### ⭐ **1. Serial GC**

* Single-threaded
* Simple, predictable
* Best for **small apps**, limited memory
  Enable with: `-XX:+UseSerialGC`

### ⭐ **2. Parallel GC** (default before Java 9)

* Uses multiple threads for Minor GC
* Good throughput for multi-core systems
  Enable: `-XX:+UseParallelGC`

### ⭐ **3. CMS (Concurrent Mark Sweep) — Deprecated**

* Concurrent (less pause time)
* Replaced by G1 GC in modern Java
* Not used in newer Java versions

### ⭐ **4. G1 GC (Garbage First) — Modern Default**

* Default from Java 9+
* Region-based heap
* Predictable pause times
* Good for large heap applications
  Enable explicitly: `-XX:+UseG1GC`

### ⭐ **5. ZGC (Z Garbage Collector)**

* Ultra-low pause times (<10ms)
* For **very large heaps** (multi-GB)
* Mostly concurrent
  Enable: `-XX:+UseZGC`

### ⭐ **6. Shenandoah GC** (for OpenJDK)

* Also low-pause collector
* Competes with ZGC

---

## 5️⃣ **GC Phases (General Idea)**

### **1. Mark Phase**

JVM marks all reachable objects.

### **2. Sweep / Cleanup**

Unmarked objects are reclaimed.

### **3. Compact (optional, collector-dependent)**

Compacts heap to avoid fragmentation.

---

## 6️⃣ **When does Full GC happen?**

* Old generation is full
* Metaspace is full
* System.gc() is called (not recommended)
* Many long-lived objects
* Large arrays or memory pressure

Full GC is **slow** → causes application pause.

---

## 7️⃣ **System.gc() — Should you use it?**

**No.**
It is *just a request* to JVM; it may trigger a costly Full GC.

Interview answer:

> “System.gc() is only a suggestion. JVM decides whether to run GC. It’s best avoided because it may cause long pauses.”

---

## 8️⃣ **Weak, Soft, Phantom References (Interview Favorite)**

| Reference Type        | GC Behavior                       | Use Case                           |
| --------------------- | --------------------------------- | ---------------------------------- |
| **Strong Reference**  | Never collected                   | Normal objects                     |
| **Soft Reference**    | Collected only when memory is low | Caches                             |
| **Weak Reference**    | Collected in next GC cycle        | Maps (WeakHashMap keys)            |
| **Phantom Reference** | Collected after finalization      | Cleanup, tracking object lifecycle |

---

## 9️⃣ **finalize() — Deprecated**

* Was called before object removal
* Not reliable
* Deprecated since Java 9, removed in Java 18
* Use **try-with-resources** or **cleaner API** instead

Interview one-liner:
**“finalize() is unreliable, slow, and deprecated — avoid using it.”**

---

## 🔟 **Common Interview Questions (with one-line answers)**

### 1. **What triggers Garbage Collection?**

Memory pressure, full young gen/old gen, or JVM decision.

### 2. **Difference between Minor GC and Major/Full GC?**

Minor = Young gen only (fast).
Major/Full = Old gen + entire heap (slow).

### 3. **Why do we need G1 GC?**

To get predictable low pause times for large heaps.

### 4. **Can you force GC?**

No — only request via System.gc(); JVM decides.

### 5. **What is a memory leak in Java?**

Holding references unintentionally so objects aren’t collected.

---

## ✔ Quick Summary (Fast Recall)

* GC removes unreachable objects → prevents memory leaks
* Heap = Young Gen (Eden + S0 + S1) + Old Gen
* Minor GC = fast, Full GC = slow
* Modern collectors: G1 (default), ZGC, Shenandoah
* finalize() deprecated — don’t use
