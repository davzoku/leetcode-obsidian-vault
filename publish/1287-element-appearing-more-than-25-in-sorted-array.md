---
last_reviewed: 2023-12-12
title: 128 Element Appearing More Than 25% In Sorted Array - Easy
excerpt: "-"
tags:
  - solution
  - arrays
---
## Problem:
Given an integer array **sorted** in non-decreasing order, there is exactly one integer in the array that occurs more than 25% of the time, return that integer.

**Example 1:**

**Input:** arr = [1,2,2,6,6,6,6,7,10]
**Output:** 6

**Example 2:**

**Input:** arr = [1,1]
**Output:** 1

**Constraints:**

- `1 <= arr.length <= 104`
- `0 <= arr[i] <= 105`

### Problem Analysis:
- Let `n` be the length of the array.
- The loop iterates through n − quarter elements, where quarter is 1/4 of the array length.
- The time complexity isO(n) because the loop runs through the array once.
- The space complexity is O(1) as the algorithm uses a constant amount of extra space.

## Solutions:

```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        n = len(arr)
        quarter = n // 4
        for i in range(n - quarter):
            if arr[i] == arr[i + quarter]:
                return arr[i]
```

## Similar Questions