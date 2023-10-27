---
last_reviewed: 2023-10-27
title: 219 Contains Duplicate II
excerpt: "-"
tags:
  - solution
  - sliding-window
---
## Problem:

Given an integer array `nums` and an integer `k`, return `true` _if there are two **distinct indices**_ `i` _and_ `j` _in the array such that_ `nums[i] == nums[j]` _and_ `abs(i - j) <= k`.

**Example 1:**

**Input:** nums = [1,2,3,1], k = 3
**Output:** true

**Example 2:**

**Input:** nums = [1,0,1,1], k = 1
**Output:** true

**Example 3:**

**Input:** nums = [1,2,3,1,2,3], k = 2
**Output:** false

**Constraints:**

- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `0 <= k <= 105`
### Problem Analysis:

- different approach from [[217-contains-duplicate]]
- need to use sliding window strategy

## Solutions:

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window = set()
        L = 0

        for R in range(len(nums)):
            if R - L > k:
                # remove the window from the left
                window.remove(nums[L])
                L += 1
            if nums[R] in window:
                return True
            # shift window to right
            window.add(nums[R])```

## Similar Questions
[[217-contains-duplicate]]