---
last_reviewed: 2023-12-07
title: 1903 Largest Odd Number in String - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
You are given a string `num`, representing a large integer. Return _the **largest-valued odd** integer (as a string) that is a **non-empty substring** of_ `num`_, or an empty string_ `""` _if no odd integer exists_.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

**Input:** num = "52"
**Output:** "5"
**Explanation:** The only non-empty substrings are "5", "2", and "52". "5" is the only odd number.

**Example 2:**

**Input:** num = "4206"
**Output:** ""
**Explanation:** There are no odd numbers in "4206".

**Example 3:**

**Input:** num = "35427"
**Output:** "35427"
**Explanation:** "35427" is already an odd number.

**Constraints:**

- `1 <= num.length <= 105`
- `num` only consists of digits and does not contain any leading zeros.

### Problem Analysis:
- Simple for loop starting from the last digit
- return result if the current digit is odd. if no odd digit is found, return an empty string

- Slight optimisation can be to hard code `[1,3,5,7,9]` to avoid converting the str to digit for every element.

- Time Complexity: O(n) worse case where n is the length of the entire string
- Space Complexity: O(1)

## Solutions:

```python
class Solution:
    def largestOddNumber(self, num: str) -> str:
        for i in range(len(num) - 1, -1, -1):
            if int(num[i]) % 2 != 0:
                return num[:i + 1]
        return ""
```

## Similar Questions