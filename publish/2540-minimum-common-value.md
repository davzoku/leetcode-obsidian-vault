---
last_reviewed: 2024-03-09
title: 2540 Minimum Common Value - Easy
excerpt: "-"
tags:
  - solution
  - two-pointers
---
## Problem:
Given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, return _the **minimum integer common** to both arrays_. If there is no common integer amongst `nums1` and `nums2`, return `-1`.

Note that an integer is said to be **common** to `nums1` and `nums2` if both arrays have **at least one** occurrence of that integer.

**Example 1:**

**Input:** nums1 = [1,2,3], nums2 = [2,4]
**Output:** 2
**Explanation:** The smallest element common to both arrays is 2, so we return 2.

**Example 2:**

**Input:** nums1 = [1,2,3,6], nums2 = [2,3,4,5]
**Output:** 2
**Explanation:** There are two common elements in the array 2 and 3 out of which 2 is the smallest, so 2 is returned.

**Constraints:**

- `1 <= nums1.length, nums2.length <= 105`
- `1 <= nums1[i], nums2[j] <= 109`
- Both `nums1` and `nums2` are sorted in **non-decreasing** order.

### Problem Analysis:
1. **High-Level Strategy:** This solution employs a two-pointer approach to find the common element between two sorted arrays `nums1` and `nums2`. Both pointers (`i` and `j`) initially start at the beginning of each array. Then, it iterates through both arrays simultaneously, comparing elements at the current pointers. If the elements are equal, it returns the common element. If the element at `nums1[i]` is smaller, it increments `i` to move to the next element in `nums1`. If the element at `nums2[j]` is smaller, it increments `j` to move to the next element in `nums2`. This process continues until either a common element is found or one of the arrays is exhausted.
    
2. **Complexity:**
    - Time Complexity: The time complexity of this solution is O(min(N, M)), where N is the length of `nums1` and M is the length of `nums2`. Since both pointers increment in each iteration and only move forward, the algorithm runs in linear time with respect to the length of the smaller array.
    - Space Complexity: The space complexity is O(1) as the algorithm only uses a constant amount of extra space regardless of the input size.

## Solutions:

```python
class Solution:
    def getCommon(self, nums1: List[int], nums2: List[int]) -> int:
        i = j = 0

        while i < len(nums1) and j < len(nums2):
            if nums1[i] == nums2[j]:
                return nums1[i]
            elif nums1[i] < nums2[j]:
                i +=1
            else:
                j +=1

        return -1
```

## Similar Questions
- [[349-intersection-of-two-arrays]]
- [[350-intersection-of-two-arrays-ii]]