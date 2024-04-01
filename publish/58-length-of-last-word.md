---
last_reviewed: 2024-04-01
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Given a string `s` consisting of words and spaces, return _the length of the **last** word in the string._

A **word** is a maximal substring consisting of non-space characters only.

**Example 1:**

**Input:** s = "Hello World"
**Output:** 5
**Explanation:** The last word is "World" with length 5.

**Example 2:**

**Input:** s = "   fly me   to   the moon  "
**Output:** 4
**Explanation:** The last word is "moon" with length 4.

**Example 3:**

**Input:** s = "luffy is still joyboy"
**Output:** 6
**Explanation:** The last word is "joyboy" with length 6.

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of only English letters and spaces `' '`.
- There will be at least one word in `s`.
### Problem Analysis:
1. High-level Strategy:
   This solution uses Python's string manipulation methods to solve the problem. Here's a breakdown of the steps:
   - `s.strip()`: This removes any leading or trailing whitespace from the string. This step ensures that we don't count any trailing spaces at the end of the string as part of the last word.
   - `split(" ")`: This splits the string into a list of substrings based on the space character. As a result, we get a list of words.
   - `[-1]`: This index retrieves the last element of the list, which represents the last word in the original string.
   - `len()`: Finally, the length of the last word is computed and returned.

2. Complexity:
   - Let's denote the length of the input string `s` as `n`.
   - `strip()`: This operation has a complexity of O(k), where `k` is the number of leading and trailing spaces. In the worst case, it could be O(n).
   - `split(" ")`: This operation splits the string into words based on spaces. It has a complexity of O(n) since it iterates over each character of the string.
   - Indexing to get the last element of the list has a complexity of O(1).
   - `len()`: This operation computes the length of the last word, which could be at most `n` characters long. Thus, it has a complexity of O(n).
   - Overall, the time complexity of the solution is O(n), where `n` is the length of the input string. The space complexity is also O(n) due to the space needed for the split list.

## Solutions:

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        return len(s.strip().split(" ")[-1])
```

## Similar Questions