# 🧩 **Question 1**

### **Find the second largest element in an array.**

### **Requirements:**

* Do **NOT** sort the array.
* Do it in **one pass** (O(n) time).
* Handle cases like:

  * Duplicate largest values
  * All values equal
  * Array too small

```java
int max = Integer.MIN_VALUE;
int secondMax = Integer.MIN_VALUE;

if (a.length < 2) {
    return -1; // or throw exception: no second largest
}

for (int i = 0; i < a.length; i++) {

    if (a[i] > max) {
        secondMax = max;
        max = a[i];
    }
    else if (a[i] > secondMax && a[i] != max) {
        secondMax = a[i];
    }
}

return secondMax;
```
**Time Complexity:** O(n)  **Space Complexity:** O(1)

---

# 🧩 **Question 2 — Check if a string is a palindrome.**

### Requirements:

* Do NOT use reverse() function.
* Use two-pointer technique.
* Ignore spaces and case (optional — your choice).
* Return true/false.

Example:
Input: `"A man a plan a canal Panama"`
Output: `true`

```java
String s = "A man a plan a canal Panama".toLowerCase();
int l = 0, r = s.length() - 1;

while (l < r) {

    if (!Character.isLetter(s.charAt(l))) {
        l++;
        continue;
    }

    if (!Character.isLetter(s.charAt(r))) {
        r--;
        continue;
    }

    if (s.charAt(l) != s.charAt(r)) {
        System.out.println("False");
        return;
    }

    l++;
    r--;
}

System.out.println("True");

```

⭐ Time complexity: O(n)
⭐ Space complexity: O(1)

```
🧩 Question 3 — Move all zeros to the end of the array (maintain order).
Example:

Input:
{0, 1, 0, 3, 12}
Output:
{1, 3, 12, 0, 0}

Requirements:

Must be in-place

Must maintain non-zero order

O(n) time

O(1) space
```
<details> <summary><h1>Key Logic</h1></summary>
Idea:
Use two pointers:

nz (non-zero pointer): scans the array from left to right

z (zero pointer): tracks the position where the next non-zero should be placed

Steps:

Start both pointers at the beginning.

Move nz through the array.

Each time you find a non-zero, swap it with the value at index z, then increment z.

In the end, all zeros automatically end up at the end while preserving the order of others.

Time: O(n)
Space: O(1)
</details>
<details><summary><h1>First approach</h1></summary>
  
```java
   int[] a = {1,0,2,3,0,4};
        int[] a = {0,0,0};
        int z=0, nz=1;
        while(nz < a.length ){
            if( a[z] ==0 && a[nz] != 0){
                int temp = a[z];
                a[z] = a[nz];
                a[nz] = temp;
                z++;
            }
            if(a[z] != 0) z++;
            nz++;
        }
        for( int i=0; i< a.length; i++)
        System.out.println(a[i]);
                   
```
              
</details>

```java
int[] a = {1, 0, 2, 3, 0, 4};

int pos = 0;  // position to place the next non-zero

for (int i = 0; i < a.length; i++) {
    if (a[i] != 0) {
        int temp = a[pos];
        a[pos] = a[i];
        a[i] = temp;
        pos++;
    }
}

```

```
Question 4 — Remove duplicate characters from a string (preserve order).
Input:

"programming"

Output:

"progamin"

Requirements:

Do NOT use HashSet directly (if writing on paper).

You may use a boolean frequency array like boolean[256].

O(n) time allowed.

Maintain original order.
```
```java
StringBuilder sb = new StringBuilder();
        String s = "programming";
        int n = s.length();
        for( int i=0; i<n; i++){
            char c = s.charAt(i);
            if( sb.indexOf(String.valueOf(c))== -1)
                sb.append(c);
        }
        System.out.println(sb.toString());
```
# ❌ **Issue 1 — Time Complexity is O(n²)**

This part is the problem:

```java
sb.indexOf(String.valueOf(c))
```

`indexOf()` is O(n), and you call it inside a loop of n iterations → total **O(n²)**.

---

# ❌ **Issue 2 — Using StringBuilder for search is not efficient**

 treating `sb` like a "set", but scanning it every time is slow.

---
For small inputs, it works perfectly.

---

# ⭐ **Approach (O(n)**

Use a boolean frequency array.

```java
String s = "programming";
boolean[] seen = new boolean[256];
StringBuilder sb = new StringBuilder();

for (int i = 0; i < s.length(); i++) {
    char c = s.charAt(i);
    if (!seen[c]) {
        seen[c] = true;
        sb.append(c);
    }
}

System.out.println(sb.toString());
```
# 🧩 **Question 5 — Find the first non-repeating character in a string**

### Example:

Input: `"swiss"`
Output: `'w'`

### Requirements:

* O(n) time
* Preserve order
* You can use frequency array or HashMap
* Print the character or return it

```java
String s = "swiss";
LinkedHashMap<Character, Integer> map = new LinkedHashMap<>();

for (int i = 0; i < s.length(); i++) {
    char c = s.charAt(i);
    map.put(c, map.getOrDefault(c, 0) + 1);
}

for (Map.Entry<Character, Integer> entry : map.entrySet()) {
    if (entry.getValue() == 1) {
        System.out.println(entry.getKey());
        return;
    }
}

System.out.println("No non-repeating character");
```

---

# ⭐ **Even Simpler Version Using Frequency Array (O(n))**


```java
String s = "swiss";

int[] freq = new int[256];

for (int i = 0; i < s.length(); i++) {
    freq[s.charAt(i)]++;
}

for (int i = 0; i < s.length(); i++) {
    if (freq[s.charAt(i)] == 1) {
        System.out.println(s.charAt(i));
        return;
    }
}
```

#  **Question 6 — Valid Parentheses (Bracket Matching)**

Given a string containing brackets `'(){}[]'`, determine if it is valid.

### Examples:

✔ `"(){}[]"` → true
✔ `"([{}])"` → true
✖ `"([)]"` → false
✖ `"((("` → false

### Requirements:

* Use a stack
* O(n) time
* Return true/false

```java
static boolean isValid(String s) {
    ArrayDeque<Character> st = new ArrayDeque<>();

    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);

        if (c == '(' || c == '{' || c == '[') {
            st.push(c);
        } else {
            if (st.isEmpty()) return false;

            char t = st.pop();

            if ((t == '(' && c != ')') ||
                (t == '{' && c != '}') ||
                (t == '[' && c != ']')) {
                return false;
            }
        }
    }

    return st.isEmpty();
}
```
Question 7 — Check if Two Strings Are Anagrams
Definition:

Two strings are anagrams if they contain the same characters in the same frequency.

Example:

Input:
"listen", "silent"
Output:
true

Requirements:

Ignore case

Do not use sorting (unless you want — but try frequency method)

O(n) solution

Use int[256] or int[26]
```java
static boolean isAna(String s1, String s2) {

    if (s1.length() != s2.length()) return false;

    s1 = s1.toLowerCase();
    s2 = s2.toLowerCase();

    int[] freq = new int[26];

    for (int i = 0; i < s1.length(); i++) {
        freq[s1.charAt(i) - 'a']++;
        freq[s2.charAt(i) - 'a']--;
    }

    for (int x : freq) {
        if (x != 0) return false;
    }

    return true;
}
```
Question 8 — Two Sum in a Sorted Array (Two Pointers)

Given a sorted array of integers and a target sum, return true if a pair exists whose sum equals the target.

Example

Input:
{1, 2, 4, 7, 11}
target = 9

Output:
true (because 2 + 7 = 9)

Requirements:

Use two-pointer approach (no HashSet)

O(n) time

No extra space
```java
static boolean twoSumSorted(int[] a, int target) {
    int l = 0;
    int r = a.length - 1;

    while (l < r) {
        int sum = a[l] + a[r];

        if (sum == target) return true;

        if (sum < target) l++;  // need a bigger sum
        else r--;               // need a smaller sum
    }

    return false;
}
```
Question 9 — Find Missing Number in 1..n

Given an array of size n containing numbers from 1 to n+1,
with exactly one number missing, find the missing number.

Example:

Input: {1, 2, 4, 5, 6}
Output: 3

Requirements:

O(n) time

O(1) space

Do NOT sort the array

Use either:

Sum formula

XOR method (better)
```java
int[] a = {1, 2, 4, 5, 6}; // missing = 3

int n = a.length;  // n = 5
int sum = 0;

for (int x : a) sum += x;

int total = (n + 1) * (n + 2) / 2; // sum of 1..6
int missing = total - sum;

System.out.println(missing);
```
XOR method
```java
int[] a = {1, 2, 4, 5, 6};

int xor = 0;
int n = a.length;

// XOR all numbers from 1 to n+1
for (int i = 1; i <= n + 1; i++)
    xor ^= i;

// XOR all array elements
for (int x : a)
    xor ^= x;

System.out.println(xor);
```
Question 10 — Find First Repeating Element in an Array

Example:
Input:
{10, 5, 3, 4, 3, 5, 6}
Output:
5 (because first repeating when scanning left-to-right is 5)

Requirements:

Return the element (not index)

O(n) time

Use HashSet or boolean array

No sorting
```java
for (int x : a) {
    if (set.contains(x)) {
        return x;
    }
    set.add(x);
}
return -1;
```
Question 12 — Stock Buy and Sell (Max Profit in One Transaction)
Given:
prices = [7, 1, 5, 3, 6, 4]
Find the maximum profit possible by buying on one day and selling later.
Expected:
5 (buy at 1, sell at 6)

I'll scan the array once.
For each price:
I update minPrice if this price is lower.
Otherwise, I compute the profit if I sell today (price - minPrice).
I keep track of the maximum profit seen so far.
This works because at every step the minPrice is guaranteed to be before the current price

```java
int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;
    int maxProfit = 0;

    for (int p : prices) {
        if (p < minPrice)
            minPrice = p;
        else
            maxProfit = Math.max(maxProfit, p - minPrice);
    }

    return maxProfit;
}
```


Kadane’s Algorithm — Maximum Subarray Sum
Question:
Given an array of integers (can contain negative numbers), find the maximum possible sum of any contiguous subarray.
Example:
[-2,1,-3,4,-1,2,1,-5,4]
Output:
6   // (4 + -1 + 2 + 1)

Logic (explained in interview):

Maintain two variables:

currentSum → sum of the current subarray

maxSum → best subarray sum found so far

Traverse the array:

Add each element to currentSum.

If currentSum becomes less than the element itself,
→ restart from that element

Update maxSum if currentSum is larger

Return maxSum.

This works because:

Any negative running sum should be discarded immediately.

```java
int maxSubArray(int[] a) {
    int maxSum = Integer.MIN_VALUE;
    int currentSum = 0;

    for (int x : a) {
        currentSum += x;
        maxSum = Math.max(maxSum, currentSum);

        if (currentSum < 0)
            currentSum = 0;
    }

    return maxSum;
}
```
Question 13 — Merge Overlapping Intervals

Input:

[[1,3], [2,6], [8,10], [15,18]]


Output:

[[1,6], [8,10], [15,18]]

Required:

Sort intervals by start

Merge if overlapping

O(n log n)


“First, sort all intervals by their start times.
Then scan them one by one.
I keep a current interval (start, end).
For each next interval:

If its start is less than or equal to the current end → they overlap → so I merge by taking:

newStart = currentStart

newEnd = max(currentEnd, nextEnd)

Otherwise (no overlap), I add the current interval to the result list and move on to the next one.

At the end, I also add the last current interval to the result.”

```java
List<int[]> merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

    List<int[]> result = new ArrayList<>();

    int start = intervals[0][0];
    int end = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {
        int currStart = intervals[i][0];
        int currEnd = intervals[i][1];

        if (currStart <= end) {
            // merge
            end = Math.max(end, currEnd);
        } else {
            result.add(new int[]{start, end});
            start = currStart;
            end = currEnd;
        }
    }

    result.add(new int[]{start, end});
    return result;
}
```

Question 14 — Find Duplicate Number in Array (1 to n)

You are given an array of size n+1 with numbers from 1 to n.
Exactly one number is duplicated multiple times.

Example:

[1, 3, 4, 2, 2]
Output: 2

Constraints:

Cannot modify the array

O(1) extra space

O(n) time

Find the duplicate

👉 Hint: Use Floyd’s Cycle Detection (Tortoise and Hare).
```java
int findDuplicate(int[] nums) {
    int slow = nums[0];
    int fast = nums[0];

    // Phase 1: find intersection point in the cycle
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    // Phase 2: find entrance to the cycle
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }

    return slow; // or fast
}
```
Find the longest substring without repeating characters

Example:

"abcabcbb" → 3  (abc)
"bbbbb" → 1
"pwwkew" → 3 (wke)


Traverse string once

Use HashSet

If duplicate appears → shrink window from left until duplicate removed

Track max window size

```java
int lengthOfLongestSubstring(String s) {
    HashSet<Character> set = new HashSet<>();
    int l = 0, maxLen = 0;

    for (int r = 0; r < s.length(); r++) {
        char c = s.charAt(r);

        while (set.contains(c)) {
            set.remove(s.charAt(l));
            l++;
        }

        set.add(c);
        maxLen = Math.max(maxLen, r - l + 1);
    }

    return maxLen;
}
```
