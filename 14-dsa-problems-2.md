#  **1️⃣ FIRST OCCURRENCE OF A TARGET (Binary Search Variant)**

### ❓ Question

Given a **sorted** array, find the **first index** where a given target appears.
If not found → return `-1`.

Example:

```
a = [2, 4, 4, 4, 6, 7]
target = 4
Output = 1
```

---

### ⭐ **Logic (Explanation)**

> I use binary search.
> When I find the target, I **don't stop**.
> I move `right` to `mid – 1` to check if there is an earlier occurrence.
> I store the possible answer in a variable.
> If the mid-value is smaller, I move right; if larger, I move left.
> Time = O(log n).

---

### ⭐ **Java Code**

```java
int firstOccurrence(int[] a, int target) {
    int l = 0, r = a.length - 1;
    int ans = -1;

    while (l <= r) {
        int mid = l + (r - l) / 2;

        if (a[mid] == target) {
            ans = mid;
            r = mid - 1;    // keep searching left
        } else if (a[mid] < target) {
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return ans;
}
```

---

# ⭐ **2️⃣ LAST OCCURRENCE OF A TARGET**

### ❓ Question

Find the **last index** where a target appears.

Example:

```
a = [2, 4, 4, 4, 6, 7]
target = 4
Output = 3
```

---

### ⭐ **Logic**

> Very similar to first occurrence.
> When I find the target, I store it but move `left = mid + 1` to find a later one.

---

### ⭐ **Java Code**

```java
int lastOccurrence(int[] a, int target) {
    int l = 0, r = a.length - 1;
    int ans = -1;

    while (l <= r) {
        int mid = l + (r - l) / 2;

        if (a[mid] == target) {
            ans = mid;
            l = mid + 1;    // keep searching right
        } else if (a[mid] < target) {
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return ans;
}
```

---

# ⭐ **3️⃣ COUNT OCCURRENCES OF TARGET**

### ❓ Question

Count how many times a target appears in a sorted array.

Example:

```
a = [1,2,2,2,3,4]
target = 2
Output = 3
```

---

### ⭐ **Logic**

> Count = lastOccurrence - firstOccurrence + 1
> If first occurrence = -1, element does not exist.

---

### ⭐ **Java Code**

```java
int countOccurrences(int[] a, int target) {
    int first = firstOccurrence(a, target);
    if (first == -1) return 0;

    int last = lastOccurrence(a, target);
    return last - first + 1;
}
```

(Uses the two functions above.)

---

# ⭐ **4️⃣ SQUARE ROOT USING BINARY SEARCH**

Compute `floor(sqrt(n))` using binary search.

### ❓ Example

```
n = 17
Output = 4
```

---

### ⭐ **Logic**

> I binary search on the answer range from 0 to n.
> For a mid value, if mid² is too large, move left.
> If mid² is <= n, store it as a possible answer and move right to find a larger valid mid.

---

### ⭐ **Java Code**

```java
int sqrtBinary(int n) {
    int l = 0, r = n;
    int ans = -1;

    while (l <= r) {
        int mid = l + (r - l) / 2;
        long sq = (long) mid * mid;

        if (sq == n) return mid;

        if (sq < n) {
            ans = mid;  // possible answer
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return ans;
}
```
---
#  **2️⃣ SORTING CONCEPTS**

---

# **1. Why is Merge Sort O(n log n)?**

### ⭐Explanation:

> Merge Sort divides the array into 2 halves recursively, which takes **log n** levels.
> At each level, merging the two halves takes **O(n)** time.
> So total time = O(n) work per level × O(log n) levels = **O(n log n)**.

### ✔ Recursion depth = log n

### ✔ Work done per level = n

### ✔ Total = n log n

---

# **2. Why is Bubble Sort bad? (Why O(n²) and inefficient?)**

### ⭐  Answer:

> Bubble Sort repeatedly compares adjacent elements and swaps them.
> For each element, it may traverse the entire array → O(n).
> It repeats this n times → **O(n²)**.
> Because it performs too many comparisons and swaps, it is slow and not used in real systems.

More points to mention:

* Not efficient for large input
* Not cache-friendly
* Lots of swaps (costly operations)
* Only good for teaching, not production

---

# **3. What is Stability in Sorting?**

### ⭐ Simple Definition:

> A stable sort keeps the **relative order** of equal elements the same as in the original input.

Example:

Input (value, id):

```
(10,A), (5,B), (10,C)
```

Stable sort output:

```
(5,B), (10,A), (10,C)
```

Order of A before C is preserved.

Unstable sort may output:

```
(5,B), (10,C), (10,A)
```

### ✔ Merge Sort → Stable

### ✔ Bubble Sort → Stable

### ✔ Insertion Sort → Stable

### ❌ Quick Sort → Not stable

### ❌ Heap Sort → Not stable

---

# **4. What is In-Place Sorting?**

### ⭐  Answer:

> A sorting algorithm is **in-place** if it uses only constant extra memory — O(1) space — and sorts the array by modifying it directly.

Examples:

| Algorithm      | In-Place                | Stable |
| -------------- | ----------------------- | ------ |
| Bubble Sort    | ✔ Yes                   | ✔ Yes  |
| Selection Sort | ✔ Yes                   | ❌ No   |
| Insertion Sort | ✔ Yes                   | ✔ Yes  |
| Quick Sort     | ✔ Yes                   | ❌ No   |
| Merge Sort     | ❌ No (uses extra array) | ✔ Yes  |

---

# Summary 

* Merge Sort = O(n log n) because n work is done for log n levels.
* Bubble Sort = O(n²) and inefficient because it repeatedly scans the whole array and swaps a lot.
* Stability means equal elements retain their original order.
* In-place means only O(1) extra memory is used.

---
# ⭐ 1️⃣ Reverse Linked List

### ❓ **Question**

Reverse a singly linked list.

### ✔ Input

`1 → 2 → 3 → 4 → null`

### ✔ Output

`4 → 3 → 2 → 1 → null`

---

### ⭐ Logic

> I maintain 3 pointers: `prev`, `curr`, `next`.
> I iterate through the list and reverse each link one-by-one.
> At the end, `prev` becomes the new head.

### 🔁 Visualization

```
prev   curr   next
null ← 1 → 2 → 3 → 4
```

At each step:

* Save next node
* Reverse `curr.next = prev`
* Move `prev = curr`
* Move `curr = next`

---

### ⭐ Java Code

```java
ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;

    while (curr != null) {
        ListNode next = curr.next;  // save next
        curr.next = prev;           // reverse link
        prev = curr;                // move prev
        curr = next;                // move curr
    }

    return prev;  // new head
}
```

### ⏱ **Time:** O(n)

### 💾 **Space:** O(1)

---

# ⭐ 2️⃣ Detect Loop in Linked List (Floyd’s Cycle Algorithm)

### ❓ **Question**

Given a linked list, detect if a cycle/loop exists.

Example:

```
1 → 2 → 3 → 4 → 5
        ↑       ↓
        ← ← ← ← ←
```

---

### ⭐  Logic

> I use Floyd’s Tortoise and Hare method.
> Move `slow` by 1 step and `fast` by 2 steps.
> If they meet, a cycle exists.
> If `fast` reaches null, no cycle exists.

### 🔁 Visualization

```
slow: 1 step
fast: 2 steps

If fast == slow → cycle exists
```

---

### ⭐ Java Code

```java
boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) return false;

    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) return true;
    }

    return false;
}
```

### ⏱ Time: O(n)

### 💾 Space: O(1)

---

# ⭐ 3️⃣ Middle of Linked List

### ❓ **Question**

Find the middle node of a singly linked list.

If list has even length → return the **second middle**
(e.g., for 1→2→3→4, answer = 3)

---

### ⭐  Logic

> Use slow and fast pointers.
> Slow moves 1 step, fast moves 2 steps.
> When fast reaches end, slow is at the middle.

---

### 🔁 Visualization

```
slow: 1 step
fast: 2 steps

1 → 2 → 3 → 4 → 5
    ↑         ↑
   slow      fast
```

---

### ⭐ Java Code

```java
ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```

### ⏱ Time: O(n)

### 💾 Space: O(1)

---
# 🌳 1. Tree

A **tree** is a hierarchical data structure consisting of **nodes** connected by **edges**.

### ✅ Key Points:

1. **Root Node** – The top node of the tree.
2. **Parent & Child** – Every node (except root) has one parent. Nodes connected below it are its children.
3. **Leaf Node** – Node with no children.
4. **Edge** – Connection between parent and child.
5. **Height / Depth** – Levels in the tree.
6. **No cycles** – Tree cannot have loops.
7. **Types**:

   * Binary Tree → max 2 children per node
   * Binary Search Tree (BST) → left child < parent < right child
   * Balanced Trees (AVL, Red-Black) → keep height small for efficiency

### Example:

```
       10
      /  \
     5    15
    / \     \
   3   7     20
```

---

# 🌐 2. Graph

A **graph** is a collection of **nodes (vertices)** connected by **edges**. Unlike trees, graphs can have cycles and multiple connections.

### ✅ Key Points:

1. **Vertex (Node)** – A point in the graph.
2. **Edge** – Connection between vertices.
3. **Directed vs Undirected**:

   * Directed → edge has direction (A → B)
   * Undirected → edge has no direction (A — B)
4. **Weighted vs Unweighted**:

   * Weighted → edges have values (cost, distance)
   * Unweighted → edges have no value
5. **Cycle** – Graph may or may not have loops
6. **Connected / Disconnected**:

   * Connected → path exists between all pairs of vertices
   * Disconnected → not all vertices are connected
7. **Representation**:

   * Adjacency Matrix → 2D array
   * Adjacency List → list of lists

### Example:

Undirected graph:

```
A — B
|   |
C — D
```

---

# 🔹 Difference between Tree and Graph

| Feature      | Tree                | Graph               |
| ------------ | ------------------- | ------------------- |
| Hierarchy    | Yes                 | No                  |
| Cycles       | No                  | Can have cycles     |
| Root         | Yes                 | Not necessary       |
| Connectivity | Always connected    | May be disconnected |
| Edges        | n-1 edges (n nodes) | Can be any number   |
---
# ⭐ **4️⃣ BASIC TREE KNOWLEDGE**

---

# ⭐ 1️⃣ Tree Traversals (Inorder / Preorder / Postorder)

### Binary tree example:

```
      1
     / \
    2   3
```

Let’s define traversal orders.

---

## ✔ **Preorder (Root → Left → Right)**

**Visit order:**

1. Root
2. Left subtree
3. Right subtree

Example:

```
1 2 3
```

### Java Snippet:

```java
void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

---

## ✔ **Inorder (Left → Root → Right)**

Used heavily in BSTs because it returns **sorted order**.

Example:

```
2 1 3
```

### Java Snippet:

```java
void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

---

## ✔ **Postorder (Left → Right → Root)**

Useful for **delete**, **free memory**.

Example:

```
2 3 1
```

### Java Snippet:

```java
void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

---

# ⭐ 2️⃣ Height of a Binary Tree

### ❓ What is height?

> Height = Maximum depth from root to any leaf.

Example:

```
      1        height = 3
     / \
    2   3
   /
  4
```

Path: 1 → 2 → 4

### ✔ Height = 3

---

### ⭐ Java Code

```java
int height(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
```

Time: O(n)

---

# ⭐ 3️⃣ What is a Leaf Node?

### Definition:

> A leaf is a node with **no children**.

Example:

```
      1
     / \
    2   3
       /
      4
```

Leaves: `2`, `4`

### Simple check:

```java
boolean isLeaf(TreeNode node) {
    return node.left == null && node.right == null;
}
```

---

# ⭐ 4️⃣ BST (Binary Search Tree) Property

### ❓ What is a BST?

> A Binary Search Tree is a binary tree where:
>
> * left subtree contains values **less than** the node
> * right subtree contains values **greater than** the node
> * both subtrees are also BSTs

### Example (valid BST)

```
      8
     / \
    3   10
       /  \
      9   14
```

### Example (NOT a BST)

```
      5
     / \
    3   7
       /
      4   <-- violates rule (4 < 5 but is in right subtree)
```

---

### ⭐ Java check for valid BST 
```java
boolean isValidBST(TreeNode root, long min, long max) {
    if (root == null) return true;

    if (root.val <= min || root.val >= max)
        return false;

    return isValidBST(root.left, min, root.val) &&
           isValidBST(root.right, root.val, max);
}
```

Call:

```java
isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
```
---

# **1️⃣ Testing Basics (Manual + Automation)**

### **Manual Testing**

* **Definition:** Process of manually checking software for bugs.
* **Key points:**

  * Test cases, test scenarios
  * Types of testing: **Functional, Regression, Smoke, UAT, Integration**
  * Bug lifecycle: New → Assigned → Fixed → Retested → Closed

### **Automation Testing**

* **Tools commonly mentioned in JD:** Selenium, JUnit, TestNG
* **Basics to know:**

  * Selenium automates web browser actions
  * JUnit/TestNG for unit testing in Java
  * Assertions (`assertEquals`, `assertTrue`)
  * Advantages: Faster regression, repeatable, reduces human error
