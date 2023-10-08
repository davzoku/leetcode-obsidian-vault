---
last_reviewed: 2023-10-08
title: 896 Monotonic Array - Easy
excerpt: "-"
tags:
  - arrays
---
## Problem:

An array is **monotonic** if it is either monotone increasing or monotone decreasing.

An array `nums` is monotone increasing if for all `i <= j`, `nums[i] <= nums[j]`. An array `nums` is monotone decreasing if for all `i <= j`, `nums[i] >= nums[j]`.

Given an integer array `nums`, return `true` _if the given array is monotonic, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [1,2,2,3]
**Output:** true

**Example 2:**

**Input:** nums = [6,5,4,4]
**Output:** true

**Example 3:**

**Input:** nums = [1,3,2]
**Output:** false

**Constraints:**

- `1 <= nums.length <= 105`
- `-105 <= nums[i] <= 105`

### Problem Analysis:

- On first thought, one may consider performing 2 loops through the list; the first to check for increasing, the second for decreasing
- we can initialize 2 flags and check for both condition in one go.
- Time complexity: O(n)

## Solutions:

```python
class Solution:
    def isMonotonic(self, nums: List[int]) -> bool:
        increasing, decreasing = True, True
        for i in range(len(nums)-1):
            if nums[i] > nums[i+1]:
                decreasing = False
            elif nums[i] < nums[i+1]:
                increasing = False
        return increasing or decreasing
```

## Similar Questions