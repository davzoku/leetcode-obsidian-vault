---
last_reviewed: 2024-03-10
title: 2215 Find the Difference of Two Arrays - Easy
excerpt: "-"
tags:
  - solution
  - sets
  - arrays
---
## Problem:
Given two **0-indexed** integer arrays `nums1` and `nums2`, return _a list_ `answer` _of size_ `2` _where:_

- `answer[0]` _is a list of all **distinct** integers in_ `nums1` _which are **not** present in_ `nums2`_._
- `answer[1]` _is a list of all **distinct** integers in_ `nums2` _which are **not** present in_ `nums1`.

**Note** that the integers in the lists may be returned in **any** order.

**Example 1:**

**Input:** nums1 = [1,2,3], nums2 = [2,4,6]
**Output:** [[1,3],[4,6]]
**Explanation:**
For nums1, nums1[1] = 2 is present at index 0 of nums2, whereas nums1[0] = 1 and nums1[2] = 3 are not present in nums2. Therefore, answer[0] = [1,3].
For nums2, nums2[0] = 2 is present at index 1 of nums1, whereas nums2[1] = 4 and nums2[2] = 6 are not present in nums2. Therefore, answer[1] = [4,6].

**Example 2:**

**Input:** nums1 = [1,2,3,3], nums2 = [1,1,2,2]
**Output:** [[3],[]]
**Explanation:**
For nums1, nums1[2] and nums1[3] are not present in nums2. Since nums1[2] == nums1[3], their value is only included once and answer[0] = [3].
Every integer in nums2 is present in nums1. Therefore, answer[1] = [].

**Constraints:**

- `1 <= nums1.length, nums2.length <= 1000`
- `-1000 <= nums1[i], nums2[i] <= 1000`

### Problem Analysis:
1. **High-Level Strategy:**
    
    - The solution aims to find the differences between two lists, `nums1` and `nums2`.
    - It starts by converting both lists into sets using the `set()` function.
    - Then, it uses the `difference()` method of sets to find elements that are in `nums1` but not in `nums2` (stored in `x`), and elements that are in `nums2` but not in `nums1` (stored in `y`).
    - Finally, it returns a list containing these two sets `x` and `y`.
2. **Complexity:**
    
    - Converting `nums1` and `nums2` into sets takes O(n) and O(m) time complexity respectively, where n and m are the sizes of `nums1` and `nums2`.
    - Finding the differences between sets using the `difference()` method takes O(min(len(nums1), len(nums2))) time complexity.
    - Therefore, the overall time complexity of this solution is O(n + m).
    - The space complexity is O(n + m) as well, due to the space required to store the sets `x` and `y`.

## Solutions:

```python
class Solution:
    def findDifference(self, nums1: List[int], nums2: List[int]) -> List[List[int]]:
        x = set(nums1).difference(set(nums2))
        y = set(nums2).difference(set(nums1))
        return [x, y]
```

## Similar Questions
- [[349-intersection-of-two-arrays]]
- [[350-intersection-of-two-arrays-ii]]
- [[2248-intersection-of-multiple-arrays]]