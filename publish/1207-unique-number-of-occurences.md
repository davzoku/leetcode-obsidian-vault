---
last_reviewed: 2024-01-17
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Given an array of integers `arr`, return `true` _if the number of occurrences of each value in the array is **unique** or_ `false` _otherwise_.

**Example 1:**

**Input:** arr = [1,2,2,1,1,3]
**Output:** true
**Explanation:** The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.

**Example 2:**

**Input:** arr = [1,2]
**Output:** false

**Example 3:**

**Input:** arr = [-3,0,1,-3,1,1,1,-3,10,0]
**Output:** true

**Constraints:**

- `1 <= arr.length <= 1000`
- `-1000 <= arr[i] <= 1000`

### Problem Analysis:
### High-Level Strategy:
The high-level strategy of this solution is as follows:

- Use the `Counter` class from the `collections` module to count the occurrences of each element in the input array `arr`.
- Create a set of the values obtained from the `Counter`.
- Check if the length of the set of values is equal to the length of the values in the `Counter`. If they are equal, it means that each unique value in the original array has a unique number of occurrences.

### Complexity Analysis:
- **Time Complexity:**
  - Counting occurrences using `Counter` has a time complexity of O(n), where n is the length of the input array.
  - Creating a set and comparing lengths has a time complexity of O(k), where k is the number of unique occurrences.
  - The overall time complexity is O(n + k).

- **Space Complexity:**
  - The space complexity is dominated by the usage of the `Counter` and the set.
  - The `Counter` object requires O(n) space to store the occurrences of each element.
  - The set of values requires additional space, but in the worst case, the space required is still O(n) (if all elements have distinct occurrences).
  - The overall space complexity is O(n).

## Solutions:

```python
class Solution:
    def uniqueOccurrences(self, arr: List[int]) -> bool:
        c1 = Counter(arr)
        return len(c1.values()) == len(set(c1.values()))
```

## Similar Questions