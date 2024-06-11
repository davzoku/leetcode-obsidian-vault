---
last_reviewed: 2024-06-10
title: 1051 Height Checker - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - sorting
---
## Problem:
A school is trying to take an annual photo of all the students. The students are asked to stand in a single file line in **non-decreasing order** by height. Let this ordering be represented by the integer array `expected` where `expected[i]` is the expected height of the `ith` student in line.

You are given an integer array `heights` representing the **current order** that the students are standing in. Each `heights[i]` is the height of the `ith` student in line (**0-indexed**).

Return _the **number of indices** where_ `heights[i] != expected[i]`.

**Example 1:**

**Input:** heights = [1,1,4,2,1,3]
**Output:** 3
**Explanation:** 
heights:  [1,1,4,2,1,3]
expected: [1,1,1,2,3,4]
Indices 2, 4, and 5 do not match.

**Example 2:**

**Input:** heights = [5,1,2,3,4]
**Output:** 5
**Explanation:**
heights:  [5,1,2,3,4]
expected: [1,2,3,4,5]
All indices do not match.

**Example 3:**

**Input:** heights = [1,2,3,4,5]
**Output:** 0
**Explanation:**
heights:  [1,2,3,4,5]
expected: [1,2,3,4,5]
All indices match.

**Constraints:**

- `1 <= heights.length <= 100`
- `1 <= heights[i] <= 100`

### Problem Analysis:
### High-Level Strategy:
1. **Sorting**: The code first sorts the `heights` list using Python's built-in `sorted()` function. Sorting allows us to obtain a sorted version of the heights list, which we'll use as a reference for comparison.
  
2. **Comparison**: After sorting, the code iterates over both the sorted `heights` list and the original `heights` list simultaneously using `enumerate()`. For each corresponding pair of elements, it checks if they are different. If they are different, it increments the `count` variable.

3. **Returning Count**: Finally, the code returns the value of `count`, which represents the number of elements that are not in the correct order when compared to the sorted version of the `heights` list.

### Complexity Analysis:
- **Sorting Complexity**: The `sorted()` function has a time complexity of O(n log n), where n is the number of elements in the `heights` list. Therefore, sorting the `heights` list takes O(n log n) time.
  
- **Iterating and Comparison**: After sorting, the code iterates over the `heights` list once, performing constant-time comparisons for each element. Thus, this step has a time complexity of O(n), where n is the number of elements in the `heights` list.
  
- **Overall Complexity**: Considering the dominating factor, the overall time complexity of the solution is O(n log n) due to the sorting step. There's also additional space complexity of O(n) due to the sorted version of the `heights` list.

## Solutions:

```python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        sorted_heights = sorted(heights)
        count = sum(1 for i, x in enumerate(sorted_heights) if x != heights[i])
        return count
```

## Similar Questions