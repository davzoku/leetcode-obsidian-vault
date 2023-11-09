---
last_reviewed: 2023-11-09
title: 1759 Count Number of Homogenous Substrings - Medium
excerpt: "-"
tags:
  - solution
  - math
---
## Problem:

Given a string `s`, return _the number of **homogenous** substrings of_ `s`_._ Since the answer may be too large, return it **modulo** `109 + 7`.

A string is **homogenous** if all the characters of the string are the same.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

**Input:** s = "abbcccaa"
**Output:** 13
**Explanation:** The homogenous substrings are listed as below:
"a"   appears 3 times.
"aa"  appears 1 time.
"b"   appears 2 times.
"bb"  appears 1 time.
"c"   appears 3 times.
"cc"  appears 2 times.
"ccc" appears 1 time.
3 + 1 + 2 + 1 + 3 + 2 + 1 = 13.

**Example 2:**

**Input:** s = "xy"
**Output:** 2
**Explanation:** The homogenous substrings are "x" and "y".

**Example 3:**

**Input:** s = "zzzzz"
**Output:** 15

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase letters.

### Problem Analysis:

- Use the `groupby` function to group consecutive identical characters in the string.
- For each group, calculate the length of the group and add the count of homogeneous substrings using the formula `(n * (n+1)) // 2`.
- Keep a running total of these counts for all groups.
- Return the total count after applying the modulo operation.

- O(n) time complexity

## Solutions:

```python
class Solution:
    def countHomogenous(self, s: str) -> int:
        # formula (n * (n+1)) // 2
        MOD = 10**9 +7 
        total = 0

        for x, y in groupby(s):
            t = len(list(y))
            total += t * (t + 1) // 2

        return total % MOD```

## Similar Questions