---
last_reviewed: 2023-10-15
title: 494 Target Sum - Medium
excerpt: "-"
tags:
  - solution
  - dynamic-programming
  - memorization
---
## Problem:

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3
**Output:** 5
**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3

**Example 2:**

**Input:** nums = [1], target = 1
**Output:** 1

**Constraints:**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

### Problem Analysis:

- use dynamic programming and memorization. 
- from the first element, recursively increment the index and backtrack to look for suitable combination
- store intermediate solution in a dictionary

## Solutions:

```python
class Solution(object):
    def findTargetSumWays(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        # memorization
        dp = {} # (index, total) : # of ways

        def backtrack(i, total):
            # base case
            if i == len(nums):
                return 1 if total == target else 0
            if (i, total) in dp:
                # take from dp
                return dp[(i, total)]
            
            dp[(i, total)] = (backtrack(i+1, total + nums[i]) +
            backtrack(i + 1, total - nums[i]))

            return dp[(i, total)]

        return backtrack(0,0)
```

## Similar Questions