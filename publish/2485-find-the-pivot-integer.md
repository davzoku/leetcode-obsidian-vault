---
last_reviewed: 2024-03-13
title: 2485 Find the Pivot Integer - Easy
excerpt: "-"
tags:
  - solution
  - math
---
## Problem:
Given a positive integer `n`, find the **pivot integer** `x` such that:

- The sum of all elements between `1` and `x` inclusively equals the sum of all elements between `x` and `n` inclusively.

Return _the pivot integer_ `x`. If no such integer exists, return `-1`. It is guaranteed that there will be at most one pivot index for the given input.

**Example 1:**

**Input:** n = 8
**Output:** 6
**Explanation:** 6 is the pivot integer since: 1 + 2 + 3 + 4 + 5 + 6 = 6 + 7 + 8 = 21.

**Example 2:**

**Input:** n = 1
**Output:** 1
**Explanation:** 1 is the pivot integer since: 1 = 1.

**Example 3:**

**Input:** n = 4
**Output:** -1
**Explanation:** It can be proved that no such integer exist.

**Constraints:**

- `1 <= n <= 1000`
### Problem Analysis:
1. **High-Level Strategy**:
    
    - First, the code calculates the total sum of integers from 1 to n using the formula for the sum of an arithmetic series.
    - Then, it takes the square root of the total sum.
    - If the square root is an integer (meaning the total sum can be evenly split into two halves), it returns that integer as the pivot integer.
    - If the square root is not an integer, it means there's no valid pivot integer, so it returns -1.
2. **Complexity Analysis**:
    
    - Calculating the total sum of integers from 1 to n takes constant time, O(1), using the formula `total_sum = n * (n + 1) // 2`.
    - Finding the square root using `math.sqrt()` takes O(log n)
    - Therefore, the overall time complexity of this solution is O(log n).
    - There's no significant space complexity as only a constant amount of extra space is used for storing intermediate variables.

## Solutions:

```python
class Solution:
    def pivotInteger(self, n: int) -> int:
        total_sum = n * (n + 1) // 2 

        a = math.sqrt(total_sum)

        if a - math.ceil(a) == 0:
            return int(a)
        else:
            return -1
```

## Similar Questions