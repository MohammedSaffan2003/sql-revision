## 🔹 **1. Collection hierarchy**

**`Iterable` → `Collection` → (List, Set, Queue)**

But note:

* **Map is NOT part of Collection**, but part of the **Collections Framework**
* Map does **not** extend Collection because it stores key-value entries, not elements

---

## 🔹 **2. List Interface**

### **ArrayList**

✔ Correct: dynamic array, index access
Add:

* Default capacity 10
* Grows by **1.5x** when full
* Not thread-safe
* Best for **read-heavy** operations
* Time complexities:

  * get() – O(1)
  * add() amortized – O(1)
  * remove(index) – O(n)

### **LinkedList**

Small correction:
LinkedList is **doubly linked list** (prev + next)

Add:

* Good for insertion/deletion in middle (O(1) if node known)
* Bad for random access (O(n))
* Implements both **List & Deque**

### **Vector**

✔ Legacy
Add:

* Thread-safe (synchronized)
* Avoid using today — replaced by ArrayList

### **Stack**

✔ Extends Vector
Add:

* Also legacy
* Prefer using **ArrayDeque** for stack

---

## 🔹 **3. Queue Interface**

### **PriorityQueue**

✔ Correct: binary heap
Add:

* Default = min-heap
* Does NOT allow null
* Not thread-safe
* Time complexity:

  * insertion: O(log n)
  * poll(): O(log n)

### **Deque / ArrayDeque**

Add:

* Best implementation for **both stack & queue**
* Faster than Stack & LinkedList
* No capacity restrictions
* Null elements **not allowed**

---

## 🔹 **4. Set Interface**

### **HashSet**

✔ Uses HashMap internally
Add:

* Stores elements as **keys**, all values as `PRESENT` object
* Allows **one null**
* No order
* Time complexity O(1) average

### **TreeSet**

✔ Implements NavigableSet
Add:

* Sorted according to **natural order** or **Comparator**
* Does NOT allow null (NullPointerException)
* Red-Black Tree internally
* Time complexity O(log n)

---

## 🔹 **5. Map Interface**

### **HashMap**

Add:

* Allows **one null key**, multiple null values
* Uses array + linked list + tree (after Java 8)
* Bucket turns into TreeNode (Red-Black tree) if collisions > threshold (8)
* Time complexities:

  * get/put O(1) average
  * worst-case O(log n) after tree transformation

### **TreeMap**

Add:

* Implements NavigableMap
* Sorted by **key**
* Does NOT allow null key
* Uses Red-Black tree
* O(log n) for get/put

---

* **HashMap** → allows 1 null key, many null values
* **HashSet** → allows 1 null (because backed by HashMap)
* **TreeMap** → does NOT allow null keys (values may be null)
* **TreeSet** → does NOT allow null elements

---
##  ArrayDeque vs Stack

*"Stack is synchronized and therefore slow and legacy. ArrayDeque is faster, non-synchronized, and provides better performance for stack operations. It is the recommended modern replacement for Stack."*

---
<details>
  <summary><h1> LinkedHashSet & LinkedHashMap</h1></summary>
  
## **LinkedHashSet**

* Extends **HashSet**
* Maintains **insertion order** using a **doubly linked list** running through all entries
* Allows one null element
* Order is predictable (unlike HashSet)
* Time complexity: O(1) average (like HashSet)

**When to use?**
When you need **unique elements + iteration in the same order as inserted**.

---

## **LinkedHashMap**

* Extends **HashMap**
* Maintains **insertion order** or **access order**
  (`accessOrder=true` makes it LRU-like)
* Great for building **LRU cache**
* Allows one null key and multiple null values
* Time complexity: O(1) average

**When to use?**
When you need a map with **predictable iteration order**.
</details>

---

##  Java Collections Framework — Revision Notes

### **Hierarchy**

* `Iterable → Collection → List, Set, Queue`
* `Map` is separate (key–value), not a child of Collection

---

## **LIST**

### **ArrayList**

* Dynamic array, fast random access
* Grows by 1.5x
* Not synchronized
* Best for reads
* get(): O(1), add(): O(1)*, remove(index): O(n)

### **LinkedList**

* Doubly linked list
* Fast insert/delete
* Slow random access
* Implements List + Deque

### **Vector** (legacy)

* Synchronized, slow
* Not recommended

### **Stack** (legacy)

* Extends Vector
* Slow due to synchronization
* Use **ArrayDeque** instead

---

## **QUEUE**

### **PriorityQueue**

* Min-heap by default
* No null allowed
* add/poll: O(log n)

### **Deque / ArrayDeque**

* Best for stack + queue
* Faster than Stack and LinkedList
* No null allowed

---

## **SET**

### **HashSet**

* Unique elements
* Backed by HashMap
* Allows one null
* O(1) average

### **LinkedHashSet**

* HashSet + maintains **insertion order**
* Uses doubly linked list
* Allows one null
* O(1) average

### **TreeSet**

* Sorted (natural or comparator)
* Red-Black tree
* No null allowed
* O(log n)

---

## **MAP**

### **HashMap**

* Key-value store
* One null key allowed
* Collision uses linked list → tree (RB tree)
* O(1) average, O(log n) worst

### **LinkedHashMap**

* HashMap + maintains **insertion or access order**
* Used for **LRU cache**
* One null key allowed
* O(1) average

### **TreeMap**

* Sorted map (by key)
* Red-Black tree
* No null key
* O(log n)

Perfect one-liner ✔
Now let’s add **Concurrent Collections** — these *are* commonly asked in interviews, especially for backend roles.

I’ll follow the same pattern:

* **You don’t need to explain anything right now.**
* I’ll give you the **full interview-ready notes**, clean and GitHub-friendly.

---

# 📝 **Java Concurrent Collections**

Java provides thread-safe collections inside the package:
`java.util.concurrent`

These collections are **faster and more scalable** than old synchronized ones (Vector, Hashtable).

---

##  **1. ConcurrentHashMap**

### **Key Points**

* Thread-safe **but far faster** than Hashtable or synchronized HashMap.
* Uses **bucket-level locking** (segment locking in older versions, fine-grained locking now).
* Multiple threads can read/write **without blocking each other**.
* No null keys or values.
* Iterators are **fail-safe** (don’t throw ConcurrentModificationException).

### **When to use?**

When a high-performance thread-safe map is required.

---

##  **2. CopyOnWriteArrayList**

### **Key Points**

* Thread-safe version of ArrayList.
* On every write (add/remove), it **creates a new copy** of the underlying array.
* Reads are **very fast** (no locking).
* Iterators don’t throw ConcurrentModificationException.

### **When to use?**

* When reads are extremely frequent and writes are rare.
  (Example: notification listeners, configuration lists)

---

##  **3. CopyOnWriteArraySet**

* Backed internally by CopyOnWriteArrayList.
* Maintains **unique elements**.
* Same behavior as CopyOnWriteArrayList: write = expensive, read = fast.

---

##  **4. ConcurrentLinkedQueue**

### **Key Points**

* Lock-free, non-blocking queue.
* Fast operations for concurrent producers/consumers.
* Good for message-passing tasks.

**When to use?**
High-performance multi-threaded queues.

---

##  **5. BlockingQueue (Interface)**

Used heavily in producer–consumer patterns.

Common implementations:

### **a. ArrayBlockingQueue**

* Bounded queue (fixed size)
* Uses locks internally
* FIFO order

### **b. LinkedBlockingQueue**

* Optionally bounded
* Better throughput than ArrayBlockingQueue

### **c. PriorityBlockingQueue**

* Priority queue that is thread-safe
* Elements processed based on priority, not insertion order

### **d. SynchronousQueue**

* No storage; each insert waits for a remove
* Used in thread pool handoff

---

##  **6. ConcurrentSkipListMap / ConcurrentSkipListSet**

Sorted and thread-safe versions of TreeMap / TreeSet.

* Internally uses a **Skip List** (lock-free structure)
* Always sorted
* Scales better than a synchronized TreeMap

---

#  **Interview Tips on Concurrent Collections**

**Q: Why not use Hashtable?**

* Fully synchronized → slow
* ConcurrentHashMap is lock-partitioned → fast

**Q: Why no nulls in ConcurrentHashMap?**

* Ambiguity between “null value” and “value not present”
* Unsafe in concurrency

**Q: When would you use CopyOnWriteArrayList?**

* When reads dominate and writes are rare
* Example: event listeners, cached configs
