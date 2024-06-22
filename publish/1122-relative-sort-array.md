---
last_reviewed: 2024-06-11
title: Relative Sort Array
excerpt: "-"
tags:
  - solution
  - arrays
  - hashmap
  - sorting
---
## Problem:
  
Given two arrays `arr1` and `arr2`, the elements of `arr2` are distinct, and all elements in `arr2` are also in `arr1`.

Sort the elements of `arr1` such that the relative ordering of items in `arr1` are the same as in `arr2`. Elements that do not appear in `arr2` should be placed at the end of `arr1` in **ascending** order.

**Example 1:**

**Input:** arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
**Output:** [2,2,2,1,4,3,3,9,6,7,19]

**Example 2:**

**Input:** arr1 = [28,6,22,8,44,17], arr2 = [22,28,8,6]
**Output:** [22,28,8,6,17,44]

**Constraints:**

- `1 <= arr1.length, arr2.length <= 1000`
- `0 <= arr1[i], arr2[i] <= 1000`
- All the elements of `arr2` are **distinct**.
- Each `arr2[i]` is in `arr1`.
### Problem Analysis:
1. **High-level Strategy:**
   - The solution first creates a dictionary `pos_dict` to store the positions of elements in `arr2`.
   - It then initializes a list `counts` to keep track of the occurrences of elements in `arr2` within `arr1`.
   - It iterates through `arr1`, incrementing counts for elements present in `arr2` and storing others in `part2`.
   - It constructs `part1` by extending elements from `arr2` based on their counts.
   - It sorts `part2`.
   - Finally, it returns the concatenation of `part1` and `part2`.

2. **Complexity:**
   - Let's denote:
     - `n` as the length of `arr1`.
     - `m` as the length of `arr2`.
   - Creating `pos_dict` takes O(m) time.
   - Initializing `counts` takes O(m) time.
   - Iterating through `arr1` takes O(n) time.
   - Constructing `part1` using `zip` and `extend` takes O(m) time.
   - Sorting `part2` takes O(m log m) time.
   - Finally, concatenating `part1` and `part2` takes O(n + m) time.
   - So, the overall time complexity is O(n + m + m log m) = O(n + m log m).
   - Additional space complexity is O(m) for `pos_dict`, O(m) for `counts`, and O(m) for `part1`. Thus, the overall space complexity is O(m).

## Solutions:

```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        pos_dict = {k: v for v, k in enumerate(arr2)}
        counts = [0] * len(arr2) 
        
        part2 = []
        for num in arr1:
            if num in pos_dict:
                counts[pos_dict[num]] += 1 
            else:
                part2.append(num)
        
        part1 = []
        for num, count in zip(arr2, counts):
            part1.extend([num] * count)
        
        part2.sort()
        
        return part1 + part2 
```

## Similar Questions