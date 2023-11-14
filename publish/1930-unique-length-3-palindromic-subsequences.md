---
last_reviewed: 2023-11-14
title: 1930 Unique Length 3 Palindromic Subsequences Medium
excerpt: "-"
tags:
  - solution
---
## Problem:

Given a string `s`, return _the number of **unique palindromes of length three** that are a **subsequence** of_ `s`.

Note that even if there are multiple ways to obtain the same subsequence, it is still only counted **once**.

A **palindrome** is a string that reads the same forwards and backwards.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.

**Example 1:**

**Input:** s = "aabca"
**Output:** 3
**Explanation:** The 3 palindromic subsequences of length 3 are:
- "aba" (subsequence of "aabca")
- "aaa" (subsequence of "aabca")
- "aca" (subsequence of "aabca")

**Example 2:**

**Input:** s = "adc"
**Output:** 0
**Explanation:** There are no palindromic subsequences of length 3 in "adc".

**Example 3:**

**Input:** s = "bbcbaba"
**Output:** 4
**Explanation:** The 4 palindromic subsequences of length 3 are:
- "bbb" (subsequence of "bbcbaba")
- "bcb" (subsequence of "bbcbaba")
- "bab" (subsequence of "bbcbaba")
- "aba" (subsequence of "bbcbaba")

**Constraints:**

- `3 <= s.length <= 105`
- `s` consists of only lowercase English letters.

### Problem Analysis:
- **Initialization:**
    - Initialize a variable `res` to store the count of unique length-3 palindromic subsequences.
    - Create a set `unique_chars` to store unique characters in the input string `s`.
- **Iteration:**
    - For each unique character `k` in the set `unique_chars`, find the first and last occurrences of `k` in the string `s` using `find` and `rfind`.
- **Counting Palindromic Subsequences:**
    - If the first occurrence index is not -1, meaning the character is present in the string:
        - Increment `res` by the count of unique characters in the substring `s[first+1:last]` (excluding the characters at the first and last indices).
- **Result:**
    - Return the final count stored in `res`.

- **Time Complexity:**    
    - O(N * M), where N is the length of the input string `s`, and M is the number of unique characters in `s`.
    - The loop iterates through each unique character, and for each character, it performs `find` and `rfind` operations, which take O(N) time.
- **Space Complexity:**
    - O(M), where M is the number of unique characters in the input string.
    - The space complexity is determined by the set `unique_chars`. In the worst case, it can grow up to the number of unique characters in the string.

## Solutions:

```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        res = 0
        # characters = {chr(x) for x in range(97,123,1)}
        unique_chars = set(s)
        for k in unique_chars:
            first,last = s.find(k),s.rfind(k)
            # print(k, first, last)
            if first!=-1:
                # print(len(set(s[first+1:last])))
                res+=len(set(s[first+1:last]))
        return res
```

## Similar Questions