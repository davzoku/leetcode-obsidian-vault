---
last_reviewed: 2024-04-24
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given `n`, return the value of Tn.

**Example 1:**

**Input:** n = 4
**Output:** 4
**Explanation:**
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4

**Example 2:**

**Input:** n = 25
**Output:** 1389537

**Constraints:**

- `0 <= n <= 37`
- The answer is guaranteed to fit within a 32-bit integer, ie. `answer <= 2^31 - 1`.

### Problem Analysis:

### High Level Strategy

1. This solution utilizes memoization to avoid redundant calculations when computing the Tribonacci sequence. It starts with a dictionary `memo` initialized with the base cases of the Tribonacci sequence (0, 1, 1), which are stored as key-value pairs. When computing the Tribonacci number for a given `n`, it first checks if `n` is already in the memo dictionary. If it is, it returns the value associated with `n`. Otherwise, it recursively computes the Tribonacci number for `n-1`, `n-2`, and `n-3`, adds them up, stores the result in the memo dictionary, and returns the computed value. This approach saves time by avoiding redundant calculations, especially for larger values of `n`.

### Time Complexity

1. The time complexity of this solution is O(n), where n is the input parameter. This is because each value of `n` is computed only once and then stored in the memo dictionary for future use. The space complexity is also O(n) due to the memo dictionary, which can store at most `n` key-value pairs. Overall, this solution provides an efficient way to compute Tribonacci numbers by trading off space for time.

## Solutions:

```python
class Solution:
    def __init__(self):
        self.memo = {0: 0, 1: 1, 2: 1}

    def tribonacci(self, n: int) -> int:
        if n in self.memo:
            return self.memo[n]
            
        self.memo[n] = self.tribonacci(n-1) + self.tribonacci(n-2) + self.tribonacci(n-3)
        return self.memo[n]
```

## Similar Questions