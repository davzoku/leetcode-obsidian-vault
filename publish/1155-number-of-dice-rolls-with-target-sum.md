---
last_reviewed: 2023-12-26
title: 1155 Number of Dice Rolls With Target Sum - Medium
excerpt: "-"
tags:
  - solution
  - dynamic-programming
  - memorization
---
## Problem:
You have `n` dice, and each die has `k` faces numbered from `1` to `k`.

Given three integers `n`, `k`, and `target`, return _the number of possible ways (out of the_ `kn` _total ways)_ _to roll the dice, so the sum of the face-up numbers equals_ `target`. Since the answer may be too large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** n = 1, k = 6, target = 3
**Output:** 1
**Explanation:** You throw one die with 6 faces.
There is only one way to get a sum of 3.

**Example 2:**

**Input:** n = 2, k = 6, target = 7
**Output:** 6
**Explanation:** You throw two dice, each with 6 faces.
There are 6 ways to get a sum of 7: 1+6, 2+5, 3+4, 4+3, 5+2, 6+1.

**Example 3:**

**Input:** n = 30, k = 30, target = 500
**Output:** 222616187
**Explanation:** The answer must be returned modulo 109 + 7.

**Constraints:**

- `1 <= n, k <= 30`
- `1 <= target <= 1000`

### Problem Analysis:
**High-Level Strategy:** 

The solution uses a recursive approach with memoization (dynamic programming). The `dfs` function calculates the number of ways to obtain the target sum with a given number of dice and the remaining target value. The result is then memoized to avoid redundant calculations.

**Complexity:**

- **Time Complexity:** O(n * k * target), where n is the number of dice, k is the number of faces on each die, and target is the target sum.
- **Space Complexity:** O(n * target) for memoization.

## Solutions:

```python
class Solution:
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        MOD = 10**9 + 7
        memo = {}

        def dfs(dice, remaining_target):
            if dice == 0:
                return 1 if remaining_target == 0 else 0

            if (dice, remaining_target) in memo:
                return memo[(dice, remaining_target)]

            ways = 0
            for face in range(1, k + 1):
                if remaining_target >= face:
                    ways = (ways + dfs(dice - 1, remaining_target - face)) % MOD

            memo[(dice, remaining_target)] = ways
            return ways

        return dfs(n, target) % MOD
```

## Similar Questions