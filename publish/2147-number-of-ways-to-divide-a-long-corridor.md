---
last_reviewed: 2023-11-28
title: 2147 Number of Ways to Divide a Long Corridor - Hard
excerpt: "-"
tags:
  - solution
  - dynamic-programming
  - combinatorics
  - memorization
---
## Problem:
Along a long library corridor, there is a line of seats and decorative plants. You are given a **0-indexed** string `corridor` of length `n` consisting of letters `'S'` and `'P'` where each `'S'` represents a seat and each `'P'` represents a plant.

One room divider has **already** been installed to the left of index `0`, and **another** to the right of index `n - 1`. Additional room dividers can be installed. For each position between indices `i - 1` and `i` (`1 <= i <= n - 1`), at most one divider can be installed.

Divide the corridor into non-overlapping sections, where each section has **exactly two seats** with any number of plants. There may be multiple ways to perform the division. Two ways are **different** if there is a position with a room divider installed in the first way but not in the second way.

Return _the number of ways to divide the corridor_. Since the answer may be very large, return it **modulo** `109 + 7`. If there is no way, return `0`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/12/04/1.png)

**Input:** corridor = "SSPPSPS"
**Output:** 3
**Explanation:** There are 3 different ways to divide the corridor.
The black bars in the above image indicate the two room dividers already installed.
Note that in each of the ways, **each** section has exactly **two** seats.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/12/04/2.png)

**Input:** corridor = "PPSPSP"
**Output:** 1
**Explanation:** There is only 1 way to divide the corridor, by not installing any additional dividers.
Installing any would create some section that does not have exactly two seats.

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/12/12/3.png)

**Input:** corridor = "S"
**Output:** 0
**Explanation:** There is no way to divide the corridor because there will always be a section that does not have exactly two seats.

**Constraints:**

- `n == corridor.length`
- `1 <= n <= 105`
- `corridor[i]` is either `'S'` or `'P'`.

### Problem Analysis:
- see [Number of Ways to Divide a Long Corridor - Leetcode 2147 - Python - YouTube](https://www.youtube.com/watch?v=YOTjCd4Eyhc&t=1150s)

**Method 1 (DP):**
- form a 2d array to cache (i, seats) -> count
- recusively perform `dfs`
	- base case: if we reach the end of the corridor return 1 if seats are 2 else 0
	- if current seats count is 2 and the current position is a seat, reset count to 0 and increment by 1 for the current seat and perfom dfs
	- else if current seats count is 2 and current seat is plant, there is option to put divider or not. reset count if divider is placed. else maintain seat count and perform recursion
	- else if current seats count is not 2, increment seat count if current position is seat and perform recursion
	
- Time Complexity: O(n)
- Space Complexity: O(n)

**Method 2 (Combinatorics):**
- count all the seats available
- for every 2 seats count the distance between each pair of seats.
- multiply these values to get the combinations

- Time Complexity: O(n)
- Space Complexity: O(n)

## Solutions:
### Dynamic Programming

```python
class Solution:
    def numberOfWays(self, corridor: str) -> int:
        MOD = 10**9 + 7 
        # memorization
        cache = [[-1] * 3 for i in range(len(corridor))] # (i, seats) -> count

        def dfs(i, seats):
            if i == len(corridor):
                return 1 if seats == 2 else 0

            if cache[i][seats] != -1:
                return cache[i][seats]

            res = 0
            if seats == 2:
                if corridor[i] == "S":
                    # reset to 0 + 1 seat after counted 2 seat
                    res = dfs(i+1, 1)
                else:
                    # else if current seat is plant
                    # reset to 0 after putting divider or
                    # choose not to put divider
                    res = (dfs(i+1, 0) + dfs(i+1, 2)) % MOD
            else:
                if corridor[i] == "S":
                    # add since current is seat
                    res = dfs(i+1, seats + 1)
                else:
                    # dont add since current is plant
                    res = dfs(i+1, seats)
            cache[i][seats] = res
            return res

        return dfs(0,0)```
### Combinatorics
```python
class Solution:
    def numberOfWays(self, corridor: str) -> int:
        MOD = 10**9 + 7 
        seats = []
        for i, c in enumerate(corridor):
            if c == "S":
                seats.append(i)
        
        length = len(seats)
        # base case
        if length <2 or length %2 == 1:
            return 0
        
        res = 1
        i = 1
        # count valid combinations by counting seat pairs
        while i < length - 1:
            res = (res * (seats[i+1] - seats[i])) % MOD
            i += 2
        return res

```
## Similar Questions