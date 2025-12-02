#  **Multithreading in Java — Notes**
## ⭐ 1. **What is a Thread?**

A **thread** is the smallest unit of execution.
A Java program runs with at least **one thread (main thread)**.

---

# 2️⃣ **Process vs Thread**

| Process                             | Thread                                               |
| ----------------------------------- | ---------------------------------------------------- |
| Independent program                 | Smallest unit of execution                           |
| Has its own memory                  | Shares memory with other threads in the same process |
| Heavyweight                         | Lightweight                                          |
| Inter-process communication is slow | Communication is fast                                |

---

# 3️⃣ **Ways to Create Threads in Java**

### ✔ **1. Extending Thread class**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}

new MyThread().start();   // start() → creates a new thread
```

### ✔ **2. Implementing Runnable interface (Recommended)**

```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task executing");
    }
}

new Thread(new MyTask()).start();
```

**Why recommended?**

* Allows extending another class
* More flexible
* Used in real-world applications

### ✔ **3. Using Callable + Future (returns value)**

```java
Callable<Integer> task = () -> 10;
Future<Integer> result = Executors.newSingleThreadExecutor().submit(task);
```

Callable → returns a value and can throw checked exceptions.

---

# 4️⃣ **Thread Life Cycle**

1. **New**
2. **Runnable**
3. **Running**
4. **Blocked / Waiting / Timed Waiting**
5. **Terminated**

---

# 5️⃣ **Important Thread Methods**

| Method        | Description                               |
| ------------- | ----------------------------------------- |
| `start()`     | Creates new thread + calls `run()`        |
| `run()`       | Actual task code                          |
| `sleep(ms)`   | Temporarily pause thread                  |
| `join()`      | Wait for another thread to finish         |
| `yield()`     | Hint to give CPU to another thread        |
| `interrupt()` | Request a thread to stop waiting/sleeping |
| `isAlive()`   | Check if thread is running                |

---

# 6️⃣ **Synchronization**

### 💡 Why synchronization?

Multiple threads accessing shared data → race conditions.

### ✔ Synchronized Methods

```java
synchronized void increment() { count++; }
```

### ✔ Synchronized Block (better performance)

```java
synchronized (this) {
    count++;
}
```

### ✔ Locking Object

Monitor lock prevents simultaneous execution of critical section.

---

# 7️⃣ **Types of Synchronization**

### ✔ **Object-Level Lock**

Used on instance methods or blocks.

### ✔ **Class-Level Lock**

Used on static synchronized methods or synchronized(ClassName.class) blocks.

---

# 8️⃣ **Volatile Keyword**

Ensures:

* **Visibility** (changes are immediately written to main memory)
* **No caching issues**

Used when:

* Multiple threads read/write a shared variable
* No compound actions (i++ is NOT safe with volatile)

---

# 9️⃣ **Atomic Classes (java.util.concurrent.atomic)**

Provide lock-free thread-safe operations:

* AtomicInteger
* AtomicLong
* AtomicReference

Example:

```java
AtomicInteger count = new AtomicInteger();
count.incrementAndGet();
```

---

# 🔟 **Deadlock, Starvation, Livelock**

### ✔ **Deadlock**

Two threads waiting for each other → stuck forever.

### ✔ **Starvation**

A thread never gets CPU because others dominate.

### ✔ **Livelock**

Threads keep reacting to each other → no progress.

---

## 1️⃣1️⃣ **Thread Pools (Executor Framework)**

### Why use Thread Pools?

* Avoid creating too many threads
* Better performance
* Controlled concurrency

### Common Pools:

```java
Executors.newFixedThreadPool(10);
Executors.newCachedThreadPool();
Executors.newSingleThreadExecutor();
Executors.newScheduledThreadPool(5);
```

---

# 1️⃣2️⃣ **Callable vs Runnable**

| Runnable                       | Callable                    |
| ------------------------------ | --------------------------- |
| No return value                | Returns value               |
| Cannot throw checked exception | Can throw checked exception |
| run()                          | call()                      |

---

# 1️⃣3️⃣ **Concurrent Collections**

| Collection           | Feature                         |
| -------------------- | ------------------------------- |
| ConcurrentHashMap    | Lock-striping, high performance |
| CopyOnWriteArrayList | Thread-safe reads               |
| BlockingQueue        | Producer-consumer pattern       |

Example:

```java
BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(10);
```

---

# 1️⃣4️⃣ **Producer-Consumer (Most asked problem)**

Uses BlockingQueue.

```java
BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(5);

Producer adds → queue.put(value)  
Consumer removes → queue.take(value)
```

---

# 1️⃣5️⃣ **Synchronized vs Lock**

| synchronized       | Lock                 |
| ------------------ | -------------------- |
| Implicit           | Explicit             |
| Cannot try locking | tryLock() available  |
| Auto release       | Must manually unlock |
| Not fair           | Can be fair          |

Locks enhance flexibility.

---

# 1️⃣6️⃣ **Future vs CompletableFuture**

| Future         | CompletableFuture                  |
| -------------- | ---------------------------------- |
| Blocking get() | Non-blocking async chaining        |
| No callbacks   | Supports callbacks                 |
| No chaining    | Supports `thenApply`, `thenAccept` |

---

# ⚡ Quick Interview Summary (Rapid Revision)

* Thread creation: **Thread, Runnable, Callable**
* Thread pools: **Fixed, Cached, Single, Scheduled**
* Synchronization: **method, block, class lock**
* volatile: **visibility guarantee**
* Problems: **deadlock, starvation, livelock**
* Tools: **Atomic classes, ConcurrentHashMap, BlockingQueue**
* Advanced: **CompletableFuture** for async programming
