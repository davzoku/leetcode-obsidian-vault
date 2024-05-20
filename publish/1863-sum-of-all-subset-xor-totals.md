---
last_reviewed: 2024-05-20
title: 1863 Sum of All Subset XOR Totals - Easy
excerpt: "-"
tags:
  - solution
  - backtracking
  - combinatorics
  - bit-manipulation
  - math
---
## Problem:
The **XOR total** of an array is defined as the bitwise `XOR` of **all its elements**, or `0` if the array is **empty**.

- For example, the **XOR total** of the array `[2,5,6]` is `2 XOR 5 XOR 6 = 1`.

Given an array `nums`, return _the **sum** of all **XOR totals** for every **subset** of_ `nums`. 

**Note:** Subsets with the **same** elements should be counted **multiple** times.

An array `a` is a **subset** of an array `b` if `a` can be obtained from `b` by deleting some (possibly zero) elements of `b`.

**Example 1:**

**Input:** nums = [1,3]
**Output:** 6
**Explanation:** The 4 subsets of [1,3] are:
- The empty subset has an XOR total of 0.
- [1] has an XOR total of 1.
- [3] has an XOR total of 3.
- [1,3] has an XOR total of 1 XOR 3 = 2.
0 + 1 + 3 + 2 = 6

**Example 2:**

**Input:** nums = [5,1,6]
**Output:** 28
**Explanation:** The 8 subsets of [5,1,6] are:
- The empty subset has an XOR total of 0.
- [5] has an XOR total of 5.
- [1] has an XOR total of 1.
- [6] has an XOR total of 6.
- [5,1] has an XOR total of 5 XOR 1 = 4.
- [5,6] has an XOR total of 5 XOR 6 = 3.
- [1,6] has an XOR total of 1 XOR 6 = 7.
- [5,1,6] has an XOR total of 5 XOR 1 XOR 6 = 2.
0 + 5 + 1 + 6 + 4 + 3 + 7 + 2 = 28

**Example 3:**

**Input:** nums = [3,4,5,6,7,8]
**Output:** 480
**Explanation:** The sum of all XOR totals for every subset is 480.

**Constraints:**

- `1 <= nums.length <= 12`
- `1 <= nums[i] <= 20`


### Problem Analysis:
### 1. High-Level Strategy:
- **Backtracking**: The solution utilizes a recursive backtracking approach to generate all possible subsets of the given list `nums`.
- **XOR Calculation**: At each step in the backtracking process, it calculates the XOR of the current subset.
- **Recursive Function**: The `backtrack` function explores two options at each step:
  - Include the current element in the subset, updating the XOR value accordingly.
  - Exclude the current element from the subset, keeping the XOR value unchanged.
- **Summation**: It sums up the XOR totals obtained from all possible subsets and returns the final result.

### 2. Complexity Analysis:
- **Time Complexity**: The time complexity mainly depends on the number of subsets generated, which is \(O(2^n)\), where \(n\) is the number of elements in the input list `nums`. This is because for each element, there are two possibilities: either include it or exclude it in each subset.
- **Space Complexity**: The space complexity is \(O(n)\), where \(n\) is the depth of the recursion stack. This is because at each recursive call, there's a constant amount of additional space used to store the current XOR value and the current index in the list `nums`.

## Solutions:

```python
class Solution:
    def subsetXORSum(self, nums: List[int]) -> int:
        def backtrack(index, current_xor):
            if index == len(nums):
                return current_xor
            # Include nums[index] in the subset
            total_with = backtrack(index + 1, current_xor ^ nums[index])
            # Do not include nums[index] in the subset
            total_without = backtrack(index + 1, current_xor)
            return total_with + total_without

        # Start from the 0th index and initial XOR as 0
        return backtrack(0, 0)
```

## Similar Questions