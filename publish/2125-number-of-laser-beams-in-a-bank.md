---
last_reviewed: 2024-01-03
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Anti-theft security devices are activated inside a bank. You are given a **0-indexed** binary string array `bank` representing the floor plan of the bank, which is an `m x n` 2D matrix. `bank[i]` represents the `ith` row, consisting of `'0'`s and `'1'`s. `'0'` means the cell is empty, while`'1'` means the cell has a security device.

There is **one** laser beam between any **two** security devices **if both** conditions are met:

- The two devices are located on two **different rows**: `r1` and `r2`, where `r1 < r2`.
- For **each** row `i` where `r1 < i < r2`, there are **no security devices** in the `ith` row.

Laser beams are independent, i.e., one beam does not interfere nor join with another.

Return _the total number of laser beams in the bank_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/12/24/laser1.jpg)

**Input:** bank = ["011001","000000","010100","001000"]
**Output:** 8
**Explanation:** Between each of the following device pairs, there is one beam. In total, there are 8 beams:
 * bank[0][1] -- bank[2][1]
 * bank[0][1] -- bank[2][3]
 * bank[0][2] -- bank[2][1]
 * bank[0][2] -- bank[2][3]
 * bank[0][5] -- bank[2][1]
 * bank[0][5] -- bank[2][3]
 * bank[2][1] -- bank[3][2]
 * bank[2][3] -- bank[3][2]
Note that there is no beam between any device on the 0th row with any on the 3rd row.
This is because the 2nd row contains security devices, which breaks the second condition.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/12/24/laser2.jpg)

**Input:** bank = ["000","111","000"]
**Output:** 0
**Explanation:** There does not exist two devices located on two different rows.

**Constraints:**

- `m == bank.length`
- `n == bank[i].length`
- `1 <= m, n <= 500`
- `bank[i][j]` is either `'0'` or `'1'`.

### Problem Analysis:

### High-Level Strategy:

- the trick is that the number of lasers between 2 rows is simply the multiplication of the lasers between the 2 rows
- any empty rows can be simply ignored.

### Complexity Analysis:

- **Time Complexity:**
    
    - The algorithm iterates through each row once, and for each row, it counts the occurrences of "1". The count operation takes linear time.
    - The overall time complexity is O(N * M), where N is the number of rows and M is the average number of columns in each row.
- **Space Complexity:**
    
    - The algorithm uses a constant amount of extra space (`prev`, `curr`, `res`).
    - The space complexity is O(1).

## Solutions:

```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        prev = bank[0].count("1")

        res = 0
        for i in range(1, len(bank)):
            curr = bank[i].count("1")
            if curr > 0:
                res += prev * curr
                prev = curr

        return res
```

## Similar Questions