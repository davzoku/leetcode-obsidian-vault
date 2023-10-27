---
last_reviewed: 2023-10-07
title: 217 Contains Duplicate - Easy
excerpt: "-"
tags:
  - neetcode
  - arrays
  - solution
---
## Problem:

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** true

**Example 2:**

**Input:** nums = [1,2,3,4]
**Output:** false

**Example 3:**

**Input:** nums = [1,1,1,3,3,4,3,2,4,2]
**Output:** true

**Constraints:**

- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

### Problem Analysis:

- initialise a dictionary to keep track of each element 
- if any integer count appears more than once, return true
- Time Complexity: O(n)

## Solutions:

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        count= {}
        for n in nums:
            count[n] = count.get(n, 0) + 1
            if count[n] > 1:
                return True
        return False
```

## Similar Questions
[[219-contains-duplicate-ii]]