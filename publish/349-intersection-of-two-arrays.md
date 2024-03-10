---
last_reviewed: 2024-03-10
title: 349 Intersection of Two Arrays - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - sets
---
## Problem:
Given two integer arrays `nums1` and `nums2`, return _an array of their intersection_. Each element in the result must be **unique** and you may return the result in **any order**.

**Example 1:**

**Input:** nums1 = [1,2,2,1], nums2 = [2,2]
**Output:** [2]

**Example 2:**

**Input:** nums1 = [4,9,5], nums2 = [9,4,9,8,4]
**Output:** [9,4]
**Explanation:** [4,9] is also accepted.

**Constraints:**

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

### Problem Analysis:
1. **High-Level Strategy:**
    
    - The solution starts by converting `nums1` and `nums2` into sets using `set(nums1)` and `set(nums2)`.
    - It then uses the `intersection` method of sets to find the common elements between the two sets.
    - Finally, it returns the resulting set, which contains the intersection of `nums1` and `nums2`.
2. **Complexity Analysis:**
    
    - Converting `nums1` and `nums2` into sets takes O(n) time complexity, where n is the size of the input lists.
    - The `intersection` operation on sets has an average time complexity of O(min(len(nums1), len(nums2))), as it iterates through the smaller set.
    - In the worst-case scenario where there are no common elements, the size of the resulting set is 0.
    - Overall, the time complexity of this solution is O(n) + O(min(len(nums1), len(nums2))), which simplifies to O(n), where n is the size of the larger input list.
    - The space complexity is O(len(nums1) + len(nums2)), as sets are created for both input lists. However, since the sets are temporary and not part of the final output, we can consider the space complexity as O(n), where n is the size of the larger input list.

## Solutions:

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        #return set([value for value in nums1 if value in nums2])
        return set(nums1).intersection(set(nums2))
```

## Similar Questions
- [[350-intersection-of-two-arrays-ii]]
- [[2248-intersection-of-multiple-arrays]]
- [[2540-minimum-common-value]]