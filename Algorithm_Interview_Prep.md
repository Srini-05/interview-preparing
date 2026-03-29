# Algorithm Interview Preparation Guide

## Overview
This guide covers essential algorithms and concepts for software developers with ~3 years of experience. Interviewers expect strong fundamentals and practical usage knowledge.

---

<details>
<summary><h2>🎯 1. Searching Algorithms (VERY IMPORTANT)</h2></summary>

### ✅ Linear Search
**Concept**: Check each element one by one  
**Time Complexity**: O(n)  
**Use Case**: When data is small or unsorted

**Example**:
```java
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

### ✅ Binary Search
**Concept**: Works on sorted arrays - divide and search  
**Time Complexity**: O(log n)  
**Use Case**: Very common interview question

**Example**:
```java
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

</details>

---

<details>
<summary><h2>🔢 2. Sorting Algorithms (MUST KNOW)</h2></summary>

### ✅ Bubble Sort
**Concept**: Simple, but inefficient  
**Time Complexity**: O(n²)

### ✅ Selection Sort
**Concept**: Finds minimum and swaps  
**Time Complexity**: O(n²)

### ✅ Insertion Sort
**Concept**: Builds sorted array step by step  
**Use Case**: Good for small data

### ✅ Merge Sort (IMPORTANT)
**Concept**: Divide and conquer  
**Time Complexity**: O(n log n)

### ✅ Quick Sort (VERY IMPORTANT)
**Concept**: Fast in practice  
**Time Complexity**: Average O(n log n)

</details>
<details>
<summary><h2>🔁 3. Recursion & Backtracking</h2></summary>

### ✅ Recursion
**Concept**: Function calling itself

**Examples**:
- Factorial
- Fibonacci

```java
public int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

### ✅ Backtracking (Basic idea)
**Concept**: Try → undo → try next

**Examples**:
- Permutations
- Subsets

</details>
**Examples**:
- Permutations
- Subsets
<details>
<summary><h2>📦 4. Hashing (VERY IMPORTANT)</h2></summary>

**Concept**: Used in HashMap/HashSet for fast lookup

**Key Points**:
- hashCode()
- Collision handling
- Average O(1) lookup time

**Example**:
```java
Map<String, Integer> map = new HashMap<>();
map.put("key", 42); // O(1) average
int value = map.get("key"); // O(1) average
```

</details><String, Integer> map = new HashMap<>();
<details>
<summary><h2>🔗 5. Two Pointer & Sliding Window</h2></summary>

### ✅ Two Pointer
**Use Case**: Used in arrays  
**Example**: Pair sum problem

```java
public boolean twoSum(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return true;
        if (sum < target) left++;
        else right--;
    }
    return false;
}
```

### ✅ Sliding Window
**Use Case**: Used for subarrays  
**Very common in interviews**

</details>
}
```

<details>
<summary><h2>🌳 6. Basic Tree Algorithms</h2></summary>

### ✅ Traversals
- **Inorder**: Left → Root → Right
- **Preorder**: Root → Left → Right  
- **Postorder**: Left → Right → Root

### ✅ BFS / DFS
- **Breadth First Search**: Level by level
- **Depth First Search**: Deep first

</details>
<details>
<summary><h2>🧮 7. Greedy Algorithms (Basic Idea)</h2></summary>

**Concept**: Make best choice at each step

**Examples**:
- Activity selection
- Minimum coins

</details>
---

## 🧮 7. Greedy Algorithms (Basic Idea)
<details>
<summary><h2>🔥 8. Dynamic Programming (Basic Level)</h2></summary>

**Key Concepts**:
- Overlapping subproblems
- Memoization

**Example**: Fibonacci optimized
```java
public int fibonacciDP(int n) {
    if (n <= 1) return n;
    int[] dp = new int[n + 1];
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

</details>lic int fibonacciDP(int n) {
<details>
<summary><h2>⚙️ 9. Java Built-in Algorithms (VERY IMPORTANT)</h2></summary>

**In real projects, you use**:
- `Collections.sort()`
- `Arrays.sort()`
- `binarySearch()`

**Know**: They use optimized algorithms internally

</details>
```

---
<details>
<summary><h2>🎯 What Interviewers Expect (3 Years Experience)</h2></summary>

### MUST KNOW:
- Binary Search
- Sorting basics (Merge/Quick idea)
- HashMap working
- Time complexity (O(1), O(n), etc.)
- Recursion basics

### GOOD TO KNOW:
- Sliding window
- BFS/DFS
- Basic DP

</details> Interviewers Expect (3 Years Experience)
<details>
<summary><h2>🧠 Perfect Interview Answer</h2></summary>

**If asked: "What algorithms do you know?"**

**Say**:
> "I'm familiar with common searching and sorting algorithms like binary search, merge sort, and quick sort. I also understand hashing concepts used in HashMap, recursion, and basic techniques like sliding window and two pointers. I focus on choosing efficient algorithms based on time complexity."

### ⚠️ Interview Tips

**Don't**:
❌ List 15 algorithms rapidly  
❌ Go too deep unless asked

**Do**:
✅ Mention categories  
✅ Give 1–2 examples  
✅ Stop and let them ask

</details>
**If asked: "What algorithms do you know?"**

**Say**:
> "I'm familiar with common searching and sorting algorithms like binary search, merge sort, and quick sort. I also understand hashing concepts used in HashMap, recursion, and basic techniques like sliding window and two pointers. I focus on choosing efficient algorithms based on time complexity."

<details>
<summary><h2>🧠 What is O(1)?</h2></summary>

**Definition**: Constant time complexity

**Simple Meaning**: The operation takes same time, no matter how large the input is.

### 📦 Example
```java
// Accessing an array element
int value = arr[5]; // O(1) - direct access to index 5
```

### ⚡ Real-Life Analogy
Think of a book with page numbers:
- You want page 50
- You go directly to page 50
- No matter how big the book is → same effort
- **That's O(1)**

### 🔥 In Context of HashMap
```java
map.get(key); // O(1) average time
```
HashMap calculates hash and finds index directly.
<details>
<summary><h2>🧠 What is O(n)?</h2></summary>

**Definition**: Linear time complexity

**Simple Meaning**: The time taken increases linearly with input size.

### 📦 Example
```java
// Loop through an array
for (int i = 0; i < n; i++) {
    System.out.println(arr[i]); // O(n) - visit each element once
}
```

### ⚡ Real-Life Analogy
Searching for a name in an unsorted list:
- You may need to check each name one by one
- Worst case → check all names
- **That's O(n)**

</details>)?

**Definition**: Linear time complexity

**Simple Meaning**: The time taken increases linearly with input size.

### 📦 Example
```java
// Loop through an array
for (int i = 0; i < n; i++) {
    System.out.println(arr[i]); // O(n) - visit each element once
}
```
<details>
<summary><h2>🎯 Interview Answers for Big O</h2></summary>

**If asked: "What is O(1)?"**
> "O(1) means constant time complexity, where the execution time does not depend on input size. For example, accessing an element in an array or retrieving a value from a HashMap is typically O(1)."

**If asked: "What is O(n)?"**
> "O(n) is linear time complexity where the execution time increases proportionally with the input size. For example, iterating through an array requires O(n) time because each element is processed once."

### ⚠️ Common Mistake
❌ Saying "O(n) is slow"  
✅ It's not slow—it's just dependent on input size

</details>
| O(1) | Constant | Fastest |
| O(log n) | Logarithmic | Fast |
| O(n) | Linear | Moderate |
| O(n²) | Quadratic | Slow |

---

## 🎯 Interview Answers for Big O

**If asked: "What is O(1)?"**
> "O(1) means constant time complexity, where the execution time does not depend on input size. For example, accessing an element in an array or retrieving a value from a HashMap is typically O(1)."

**If asked: "What is O(n)?"**
> "O(n) is linear time complexity where the execution time increases proportionally with the input size. For example, iterating through an array requires O(n) time because each element is processed once."

### ⚠️ Common Mistake
❌ Saying "O(n) is slow"  
✅ It's not slow—it's just dependent on input size

---

## 🚀 Pro Tips

1. **Keep answers simple and structured**
2. **Give one definition + one example + stop**
3. **Let the interviewer ask follow-up questions**
4. **Focus on practical usage over theoretical depth**
