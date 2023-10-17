---
last_reviewed: 2023-10-17
title: 91 Decode Ways - Medium
excerpt: "-"
tags:
  - solution
  - dynamic-programming
---
## Problem:

A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:

'A' -> "1"
'B' -> "2"
...
'Z' -> "26"

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

- `"AAJF"` with the grouping `(1 1 10 6)`
- `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return _the **number** of ways to **decode** it_.

The test cases are generated so that the answer fits in a **32-bit** integer.

**Example 1:**

**Input:** s = "12"
**Output:** 2
**Explanation:** "12" could be decoded as "AB" (1 2) or "L" (12).

**Example 2:**

**Input:** s = "226"
**Output:** 3
**Explanation:** "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).

**Example 3:**

**Input:** s = "06"
**Output:** 0
**Explanation:** "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").

**Constraints:**

- `1 <= s.length <= 100`
- `s` contains only digits and may contain leading zero(s).

### Problem Analysis:
- use dynamic programming and memorization
- base case the whole string itself is 1 way of decoding
- the number of solution of `i` is composed of the number of solution found in `i+1`
- if the current char at index `i` is "1", the number of solution can be found in `i+1` and `i+2`
- similarly, if the current char `i` is "2" and the char at `i+1` is less than or equal to 6,  the number of solution can be found in `i+1` and `i+2`

## Solutions:

```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        # base case is 1 solution
        dp = {len(s):1} # length : # of soln

        def dfs (i):
            if i in dp:
                return dp[i]
            if s[i] == "0":
                return 0
            
            res = dfs(i+1)

            if (i+1 < len(s) and (s[i] == "1" or
                s[i] == "2" and s[i+1] in "0123456")):

                res += dfs(i+2)
            dp[i] = res
            return res
        return dfs(0)
```

```python
# Testcase
s= "226"

dp =
{3: 1} 
{2: 1, 3: 1} 
{1: 2, 2: 1, 3: 1} 
{0: 3, 1: 2, 2: 1, 3: 1}

output = 3
```

```python

# solution 2

class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        # base case is 1 solution
        dp = {len(s):1} # length : # of soln

        for i in range(len(s)-1, -1, -1):
            if s[i] == "0":
                dp[i] = 0 
            else:
                dp[i] = dp[i+1]
            
            if (i + 1 < len(s) and (s[i] == "1" or
                s[i] == "2" and s[i+1] in "0123456")):
                dp[i] += dp[i+2]

        return dp[0]
```
## Similar Questions