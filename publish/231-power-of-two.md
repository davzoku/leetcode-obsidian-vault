---
last_reviewed: 2023-10-24
title: 231 Power of Two - Easy
excerpt: "-"
tags:
  - solution
  - bit-manipulation
---
## Problem:
Given an integer `n`, return _`true` if it is a power of two. Otherwise, return `false`_.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

**Example 1:**

**Input:** n = 1
**Output:** true
**Explanation:** 20 = 1

**Example 2:**

**Input:** n = 16
**Output:** true
**Explanation:** 24 = 16

**Example 3:**

**Input:** n = 3
**Output:** false

**Constraints:**

- `-231 <= n <= 231 - 1`

**Follow up:** Could you solve it without loops/recursion?

### Problem Analysis:

- use recursion or
- use log or
- use bit manipulation
	- `(n & (n - 1)) == 0`: This part is the key to checking whether `n` is a power of two.
	- `n - 1` subtracts 1 from `n`. This operation flips the rightmost set bit in the binary representation of `n` to 0 while leaving all other bits the same.
	- `n & (n - 1)` performs a bitwise AND operation between `n` and `n - 1`. In this operation, the result will be zero if and only if `n` has exactly one bit set to 1 in its binary representation. This is because when you AND a number with itself minus one, all the bits to the right of the rightmost set bit become zero, and all other bits remain unchanged.

## Solutions:

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        return n>0 and (n & (n - 1)) == 0
```

or 

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        return n > 0 and int(math.log10(n) / math.log10(2)) == (math.log10(n) / math.log10(2))
```
## Similar Questions

[[326-power-of-three]]
[[342-power-of-four]]