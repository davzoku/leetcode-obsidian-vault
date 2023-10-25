---
last_reviewed: 2023-10-25
title: 326 Power of Three - Easy
excerpt: "-"
tags:
  - solution
  - bit-manipulation
---
## Problem:
Given an integer `n`, return _`true` if it is a power of three. Otherwise, return `false`_.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.

**Example 1:**

**Input:** n = 27
**Output:** true
**Explanation:** 27 = 33

**Example 2:**

**Input:** n = 0
**Output:** false
**Explanation:** There is no x where 3x = 0.

**Example 3:**

**Input:** n = -1
**Output:** false
**Explanation:** There is no x where 3x = (-1).

**Constraints:**

- `-231 <= n <= 231 - 1`

**Follow up:** Could you solve it without loops/recursion?
### Problem Analysis:

- use log; be careful of floating point issue
- or while loop

## Solutions:

```python
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        return n > 0 and int(math.log10(n) / math.log10(3)) == (math.log10(n) / math.log10(3))
```

## Similar Questions

[[231-power-of-two]]
[[342-power-of-four]]