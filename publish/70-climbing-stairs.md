---
last_reviewed: 2023-10-14
title: 70 Climbing Stairs - Easy
excerpt: "-"
tags:
  - solution
  - dynamic-programming
---
## Problem:

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

**Constraints:**

- `1 <= n <= 45`

### Problem Analysis:

- use dynamic programming, memorization. Specifically, the solution can be constructed by the previous 2 values in the memorization array, so we don't have to store the whole memorization table.

## Solutions:

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        # memorization by just rmbing the prev 2 values

        one_step, two_step = 1, 1

        for i in range(n-1):
            temp = one_step + two_step
            one_step = two_step
            two_step = temp
        
        return two_step
```

## Similar Questions