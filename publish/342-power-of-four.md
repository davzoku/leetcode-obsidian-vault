---
last_reviewed: 2023-10-23
title: 342 Power of Four - Easy
excerpt: "-"
tags:
  - solution
  - bit-manipulation
---
## Problem: 
Given an integer `n`, return _`true` if it is a power of four. Otherwise, return `false`_.

An integer `n` is a power of four, if there exists an integer `x` such that `n == 4x`.

**Example 1:**

**Input:** n = 16
**Output:** true

**Example 2:**

**Input:** n = 5
**Output:** false

**Example 3:**

**Input:** n = 1
**Output:** true

**Constraints:**

- `-231 <= n <= 231 - 1`

**Follow up:** Could you solve it without loops/recursion?
### Problem Analysis:

- use bitwise manipulation or log formula


## Solutions:

```python
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        return n>0 and log(n,4) %1 == 0
```

## Similar Questions

[[231-power-of-two]]
[[326-power-of-three]]