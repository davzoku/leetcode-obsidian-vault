---
last_reviewed: 2023-11-11
title: 14 Longest Common Prefix - Easy
excerpt: "-"
tags:
  - solution
  - string
  - trie
---
## Problem:
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = ["flower","flow","flight"]
**Output:** "fl"

**Example 2:**

**Input:** strs = ["dog","racecar","car"]
**Output:** ""
**Explanation:** There is no common prefix among the input strings.

**Constraints:**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

### Problem Analysis:

1. Iterate through characters of the first string (`strs[0]`).
2. For each character position `i`, compare it with the corresponding character in other strings.
3. If a mismatch is found or the end of any string is reached, return the substring of that string up to position `i`.
4. If no mismatches are found, return the entire first string.

- Time Complexity: O(n * m)
    - n is the length of the first string, m is the number of strings.
    - Nested loops iterate through characters of the first string and check corresponding characters in other strings.
- Space Complexity: O(1)
    - Constant extra space usage.
    - No additional data structures that scale with input size.

## Solutions:

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        for i in range(len(strs[0])):
            for j in range(1, len(strs)):
                if i == len(strs[j]) or strs[0][i] != strs[j][i]:
                    return strs[j][:i]
        return strs[0]      
```

## Similar Questions