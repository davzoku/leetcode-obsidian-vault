---
last_reviewed: 2023-10-15
title: "509"
excerpt: "-"
tags:
  - solution
  - recursion
  - dynamic-programming
---
## Problem:

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.

Given `n`, calculate `F(n)`.

**Example 1:**

**Input:** n = 2
**Output:** 1
**Explanation:** F(2) = F(1) + F(0) = 1 + 0 = 1.

**Example 2:**

**Input:** n = 3
**Output:** 2
**Explanation:** F(3) = F(2) + F(1) = 1 + 1 = 2.

**Example 3:**

**Input:** n = 4
**Output:** 3
**Explanation:** F(4) = F(3) + F(2) = 2 + 1 = 3.

**Constraints:**

- `0 <= n <= 30`

### Problem Analysis:
- can used either dynamic programming or recursion

## Solutions:

```python
class Solution(object):
    def fib(self, n):
        """
        :type n: int
        :rtype: int
        """

        one, two = 0, 1

        if n == 0:
            return one

        for i in range(n-1):
            temp = one + two
            one = two
            two = temp

        return two
```

## Similar Questions

- [[118-pascals-triangle]]
- [[198-house-robber]]
