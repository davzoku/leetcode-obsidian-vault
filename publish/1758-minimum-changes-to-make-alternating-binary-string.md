---
last_reviewed: 2023-12-25
title: 1758 Minimum Changes To Make Alternating Binary String - Easy
excerpt: "-"
tags:
  - solution
  - string
---
## Problem:
You are given a string `s` consisting only of the characters `'0'` and `'1'`. In one operation, you can change any `'0'` to `'1'` or vice versa.

The string is called alternating if no two adjacent characters are equal. For example, the string `"010"` is alternating, while the string `"0100"` is not.

Return _the **minimum** number of operations needed to make_ `s` _alternating_.

**Example 1:**

**Input:** s = "0100"
**Output:** 1
**Explanation:** If you change the last character to '1', s will be "0101", which is alternating.

**Example 2:**

**Input:** s = "10"
**Output:** 0
**Explanation:** s is already alternating.

**Example 3:**

**Input:** s = "1111"
**Output:** 2
**Explanation:** You need two operations to reach "0101" or "1010".

**Constraints:**

- `1 <= s.length <= 104`
- `s[i]` is either `'0'` or `'1'`.

### Problem Analysis:
The goal of this solution is to find the minimum number of operations needed to make a binary string (consisting of '0' and '1') either all '0's or all '1's. An operation involves flipping a consecutive subarray of characters. The strategy is to iterate through the string and count the operations needed for two possible starting points: starting with '0' and starting with '1'. The final result is the minimum of these two counts.

**Complexity:**

- **Time Complexity:** O(n), where n is the length of the input string `s`. The solution iterates through the string once.
- **Space Complexity:** O(1). The algorithm uses a constant amount of space for the `count` variable.

## Solutions:

```python
class Solution:
    def minOperations(self, s: str) -> int:
        count = 0 # operations start w 0

        for i in range(len(s)):
            if i%2:
                count += 1 if s[i] != "0" else 0
            else:
                count += 1 if s[i] != "1" else 0
        # len(s) - count: operations start w 1
        return min(count, len(s) - count)
```

## Similar Questions