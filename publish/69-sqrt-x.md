---
last_reviewed: 2023-10-18
title: 69 Sqrt(x) - Easy
excerpt: "-"
tags:
  - solution
  - binary-search
---
## Problem:
Given a non-negative integer `x`, return _the square root of_ `x` _rounded down to the nearest integer_. The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

- For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

**Example 1:**

**Input:** x = 4
**Output:** 2
**Explanation:** The square root of 4 is 2, so we return 2.

**Example 2:**

**Input:** x = 8
**Output:** 2
**Explanation:** The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.

**Constraints:**

- `0 <= x <= 231 - 1`
### Problem Analysis:

- use binary search to get O(log n)

## Solutions:

```python

class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        # use binary search to achieve O(logn) instead of
        # brute force for loop: O(sqrt(n))

        l, r = 0, x
        res = 0

        while l <= r:
            # to avoid overflow, minus l not one
            m = l + (r - l) // 2
            if m*m > x:
                r = m-1
            elif m*m < x:
                l = m+1
                res = m
            else: 
                # exact match
                return m
        return res
        l, r = 0, x
        while l <= r:
            mid = l + (r-l)//2
            if mid * mid <= x < (mid+1)*(mid+1):
                return mid
            elif x < mid * mid:
                r = mid - 1
            else:
                l = mid + 1        ```

## Similar Questions