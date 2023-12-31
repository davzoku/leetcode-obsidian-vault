---
last_reviewed: 2023-12-31
title: 1624 Largest Substring Between Two Equal Characters - Easy
excerpt: "-"
tags:
  - solution
  - hashmap
  - string
---
## Problem:
Given a string `s`, return _the length of the longest substring between two equal characters, excluding the two characters._ If there is no such substring return `-1`.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

**Input:** s = "aa"
**Output:** 0
**Explanation:** The optimal substring here is an empty substring between the two `'a's`.

**Example 2:**

**Input:** s = "abca"
**Output:** 2
**Explanation:** The optimal substring here is "bc".

**Example 3:**

**Input:** s = "cbzxy"
**Output:** -1
**Explanation:** There are no characters that appear twice in s.

**Constraints:**

- `1 <= s.length <= 300`
- `s` contains only lowercase English letters.

### Problem Analysis:

High-level strategy:

- The solution uses a dictionary (`char_index`) to store the last index at which each character is encountered.
- It iterates through the string, and for each character, it calculates the distance between the current index and the last occurrence of the character.
- It updates the result with the maximum distance found.

Complexity:

- Time Complexity: O(n), where n is the length of the input string `s`. The solution iterates through the string once.
- Space Complexity: O(1)

## Solutions:

```python
class Solution:
    def maxLengthBetweenEqualCharacters(self, s: str) -> int:
        char_index = {}
        res = -1

        for k, v in enumerate(s):
            if v in char_index:
                temp = k - char_index[v] - 1
                res = max(res, temp)
            else:
                char_index[v] = k
        return res
```

## Similar Questions