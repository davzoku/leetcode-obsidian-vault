---
last_reviewed: 2024-03-10
title: 350 Intersection of Two Arrays II - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
Given two integer arrays `nums1` and `nums2`, return _an array of their intersection_. Each element in the result must appear as many times as it shows in both arrays and you may return the result in **any order**.

**Example 1:**

**Input:** nums1 = [1,2,2,1], nums2 = [2,2]
**Output:** [2,2]

**Example 2:**

**Input:** nums1 = [4,9,5], nums2 = [9,4,9,8,4]
**Output:** [4,9]
**Explanation:** [9,4] is also accepted.

**Constraints:**

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if `nums1`'s size is small compared to `nums2`'s size? Which algorithm is better?
- What if elements of `nums2` are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### Problem Analysis:

1. **High-Level Strategy:**
    
    - The solution uses the `Counter` class from the `collections` module in Python, which creates a dictionary-like object where elements of the list are keys and their counts are values.
    - It creates two `Counter` objects, `counter1` and `counter2`, from the input lists `nums1` and `nums2` respectively.
    - Then, it computes the intersection of these counters using the `&` operator, which returns a new `Counter` containing the common elements and their minimum counts.
    - Finally, it flattens the intersection `Counter` using the `elements()` method and converts it to a list.
2. **Complexity:**
    
    - Creating the counters `counter1` and `counter2` takes O(n + m) time, where n and m are the lengths of `nums1` and `nums2` respectively, due to iterating through the input lists.
    - Computing the intersection using the `&` operator has a time complexity of O(min(n, m)), where n and m are the number of unique elements in `nums1` and `nums2` respectively.
    - Flattening the intersection using the `elements()` method has a time complexity of O(k), where k is the number of elements in the intersection.
    - Overall, the time complexity of this solution is O(n + m + min(n, m) + k), which simplifies to O(n + m) in the worst case.
    - The space complexity of this solution is O(min(n, m) + k), where k is the number of elements in the intersection, because it stores the counters and the flattened intersection.

## Solutions:

```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        counter1 = Counter(nums1)
        counter2 = Counter(nums2)
        
        intersection = counter1 & counter2
        
        return list(intersection.elements())
```

## Similar Questions
- [[349-intersection-of-two-arrays]]
- [[2248-intersection-of-multiple-arrays]]
- [[2540-minimum-common-value]]