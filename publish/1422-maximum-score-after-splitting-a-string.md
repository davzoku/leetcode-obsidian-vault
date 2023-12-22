---
last_reviewed: 2023-12-22
title: 1422 Maximum Score After Splitting a String - Easy
excerpt: "-"
tags:
  - solution
  - string
---
## Problem:
Given a string `s` of zeros and ones, _return the maximum score after splitting the string into two **non-empty** substrings_ (i.e. **left** substring and **right** substring).

The score after splitting a string is the number of **zeros** in the **left** substring plus the number of **ones** in the **right** substring.

**Example 1:**

**Input:** s = "011101"
**Output:** 5 
**Explanation:** 
All possible ways of splitting s into two non-empty substrings are:
left = "0" and right = "11101", score = 1 + 4 = 5 
left = "01" and right = "1101", score = 1 + 3 = 4 
left = "011" and right = "101", score = 1 + 2 = 3 
left = "0111" and right = "01", score = 1 + 1 = 2 
left = "01110" and right = "1", score = 2 + 1 = 3

**Example 2:**

**Input:** s = "00111"
**Output:** 5
**Explanation:** When left = "00" and right = "111", we get the maximum score = 2 + 3 = 5

**Example 3:**

**Input:** s = "1111"
**Output:** 3

**Constraints:**

- `2 <= s.length <= 500`
- The string `s` consists of characters `'0'` and `'1'` only.

### Problem Analysis:
1. Initialize `zeros` to 0, `ones` to the count of '1's in the string, and `res` to 0.
2. Iterate through the string, and for each character:
    - If it's '0', increment `zeros`.
    - If it's '1', decrement `ones`.
    - Update `res` with the maximum value of the sum of `zeros` and `ones`.
3. Return the final value of `res`.

- **Time Complexity:** O(N), where N is the length of the string. The algorithm iterates through the string once.
- **Space Complexity:** O(1). The algorithm uses a constant amount of space for variables (`zeros`, `ones`, `res`) regardless of the input size.

## Solutions:

```python
class Solution:
    def maxScore(self, s: str) -> int:
        zeros = 0
        ones = s.count("1")
        res = 0

        for i in range(len(s)-1):
            if s[i] == "0":
                zeros += 1
            else:
                ones -= 1
            res = max(res, zeros+ones)
            
        return res
```

## Similar Questions