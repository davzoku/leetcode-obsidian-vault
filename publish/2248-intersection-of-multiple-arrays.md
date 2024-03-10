---
last_reviewed: 2024-03-10
title: 2248 Intersection of Multiple Arrays
excerpt: "-"
tags:
  - solution
  - sets
  - arrays
  - sorting
---
## Problem:
Given a 2D integer array `nums` where `nums[i]` is a non-empty array of **distinct** positive integers, return _the list of integers that are present in **each array** of_ `nums` _sorted in **ascending order**_.

**Example 1:**

**Input:** nums = [[**3**,1,2,**4**,5],[1,2,**3**,**4**],[**3**,**4**,5,6]]
**Output:** [3,4]
**Explanation:** 
The only integers present in each of nums[0] = [**3**,1,2,**4**,5], nums[1] = [1,2,**3**,**4**], and nums[2] = [**3**,**4**,5,6] are 3 and 4, so we return [3,4].

**Example 2:**

**Input:** nums = [[1,2,3],[4,5,6]]
**Output:** []
**Explanation:** 
There does not exist any integer present both in nums[0] and nums[1], so we return an empty list [].

**Constraints:**

- `1 <= nums.length <= 1000`
- `1 <= sum(nums[i].length) <= 1000`
- `1 <= nums[i][j] <= 1000`
- All the values of `nums[i]` are **unique**.

### Problem Analysis:
1. **High-Level Strategy:**
    
    - The solution aims to find the intersection of multiple lists contained within the input list `nums`.
    - It starts by converting the first list in `nums` into a set using `set(nums[0])`.
    - Then, it iterates through the remaining lists in `nums[1:]`, converting each of them into sets using a list comprehension `[set(i) for i in nums[1:]]`.
    - It then uses the `intersection` method of sets to find the common elements among these sets.
    - Finally, it sorts the resulting intersection set and returns it as a list.
2. **Complexity:**
    
    - Converting the first list in `nums` into a set takes O(n) time complexity, where n is the size of the first list.
    - Converting the remaining lists in `nums[1:]` into sets using list comprehension takes O(m) time complexity, where m is the total number of elements in the remaining lists.
    - Finding the intersection of sets using the `intersection` method takes O(min(n, m)) time complexity, where n is the size of the first set and m is the total number of elements in the remaining sets.
    - Sorting the resulting intersection set takes O(k log k) time complexity, where k is the number of elements in the intersection.
    - Overall, the time complexity of this solution is O(n + m + min(n, m) + k log k).
    - The space complexity of this solution is O(min(n, m) + k), where k is the number of elements in the intersection, because it stores the sets and the resulting intersection.

## Solutions:

```python
class Solution:
    def intersection(self, nums: List[List[int]]) -> List[int]:
        return sorted(set(nums[0]).intersection(*[set(i) for i in nums[1:]]))
```

## Similar Questions
- [[349-intersection-of-two-arrays]]
- [[350-intersection-of-two-arrays-ii]]