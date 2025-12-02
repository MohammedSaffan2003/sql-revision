#  **DSA — Interview Notes (Java)**

---

# ⭐ 1. **Time & Space Complexity Basics**

* **Time Complexity (TC)** → How fast an algorithm runs relative to input size `n`.
* **Space Complexity (SC)** → Extra memory used by algorithm.

### Common complexities

| Complexity | Example                   | Notes                 |
| ---------- | ------------------------- | --------------------- |
| O(1)       | Access array index        | Constant time         |
| O(log n)   | Binary search             | Halves data each step |
| O(n)       | Linear search             | Loop through array    |
| O(n log n) | MergeSort, QuickSort      | Divide & conquer      |
| O(n²)      | BubbleSort, InsertionSort | Nested loops          |

**Interview tip:** Always mention **best, worst, average cases** for algorithms.

---

# 🔢 2. **Arrays**

### Key points

* Fixed size, contiguous memory
* Index-based access → O(1)
* Insertion/deletion in middle → O(n)

### Common interview patterns

1. **Two pointer / sliding window**

```java
// Example: find two numbers sum = target
int left = 0, right = arr.length-1;
while(left < right){
    int sum = arr[left]+arr[right];
    if(sum==target) break;
    else if(sum<target) left++;
    else right--;
}
```

2. **Prefix sum / cumulative sum**

```java
for(int i=1;i<n;i++) arr[i]+=arr[i-1];
```

3. **Rotate / Reverse array**

```java
// Reverse in place
while(start<end){
    swap(arr,start,end);
    start++; end--;
}
```

---

# 🔤 3. **Strings**

### Key points

* Immutable in Java
* Operations create new string → O(n)
* Use **StringBuilder/StringBuffer** for mutability

### Common interview patterns

* **Palindrome check**

```java
String s = "abcba";
boolean isPalindrome = s.equals(new StringBuilder(s).reverse().toString());
```

* **Anagram check**

```java
char[] c1 = s1.toCharArray(), c2 = s2.toCharArray();
Arrays.sort(c1); Arrays.sort(c2);
return Arrays.equals(c1,c2);
```

* **Frequency map (HashMap)**

```java
Map<Character,Integer> freq = new HashMap<>();
for(char ch: s.toCharArray()) freq.put(ch,freq.getOrDefault(ch,0)+1);
```

---

# 🗝 4. **HashMap / HashSet Problems**

### Why used

* Fast **lookup, insert, delete** → O(1) average
* Good for **counting/frequency**

### Common interview questions

* **Find duplicates**

```java
Set<Integer> set = new HashSet<>();
for(int x: arr){
    if(!set.add(x)) System.out.println(x);
}
```

* **Two sum**

```java
Map<Integer,Integer> map = new HashMap<>();
for(int i=0;i<arr.length;i++){
    if(map.containsKey(target-arr[i])) return new int[]{map.get(target-arr[i]),i};
    map.put(arr[i],i);
}
```

---

# 🔢 5. **Sorting**

### Common algorithms & complexity

| Algorithm     | TC Best    | TC Avg/Worst | In-place | Stable |
| ------------- | ---------- | ------------ | -------- | ------ |
| BubbleSort    | O(n)       | O(n²)        | Yes      | Yes    |
| InsertionSort | O(n)       | O(n²)        | Yes      | Yes    |
| SelectionSort | O(n²)      | O(n²)        | Yes      | No     |
| MergeSort     | O(n log n) | O(n log n)   | No       | Yes    |
| QuickSort     | O(n log n) | O(n²)        | Yes      | No     |
| HeapSort      | O(n log n) | O(n log n)   | Yes      | No     |

**Interview tip:** Know **MergeSort vs QuickSort** differences.

---

# 🧩 6. **Two Pointer / Sliding Window Patterns**

* **Use case:** Arrays / Strings problems like subarrays, sum, duplicates
* **Key idea:** Use left & right pointers to shrink/grow window
* **Examples:** max sum subarray, longest substring without repeating chars, pair sum problems

---

# 🧮 7. **Recursion & Backtracking**

* Recursion: function calls itself
* Backtracking: explore all possibilities and undo choice
* Example problems:

  * N-Queens
  * Sudoku Solver
  * Generate permutations / combinations

**Interview tip:** Always mention **base case + recursive step + complexity**.

---

# 📊 8. **Common Patterns in Interviews**

1. **Frequency counting → HashMap**
2. **Sorting + two pointers**
3. **Sliding window for subarray/subsequence**
4. **Prefix sum / cumulative sum**
5. **Recursion / DFS / Backtracking**
6. **Heap / PriorityQueue for top K problems**

---

# ⚡ Quick Revision (Rapid-fire)

* Arrays → fixed size, O(1) access
* Strings → immutable, use StringBuilder for edits
* HashMap/HashSet → fast lookup, counting
* Sorting → know O(n log n) sorts
* Sliding Window → subarray/subsequence problems
* Two Pointer → sum, pair, duplicates
* Recursion → base + recursion + unwind step
* Heap/PQ → top K / min/max problems
