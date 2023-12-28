---
last_reviewed: 2023-12-28
title: 1531 String Compression II - Hard
excerpt: "-"
tags:
  - solution
  - dynamic-programming
  - memorization
  - string
---
## Problem:
[Run-length encoding](http://en.wikipedia.org/wiki/Run-length_encoding) is a string compression method that works by replacing consecutive identical characters (repeated 2 or more times) with the concatenation of the character and the number marking the count of the characters (length of the run). For example, to compress the string `"aabccc"` we replace `"aa"` by `"a2"` and replace `"ccc"` by `"c3"`. Thus the compressed string becomes `"a2bc3"`.

Notice that in this problem, we are not adding `'1'` after single characters.

Given a string `s` and an integer `k`. You need to delete **at most** `k` characters from `s` such that the run-length encoded version of `s` has minimum length.

Find the _minimum length of the run-length encoded version of_ `s` _after deleting at most_ `k` _characters_.

**Example 1:**

**Input:** s = "aaabcccd", k = 2
**Output:** 4
**Explanation:** Compressing s without deleting anything will give us "a3bc3d" of length 6. Deleting any of the characters 'a' or 'c' would at most decrease the length of the compressed string to 5, for instance delete 2 'a' then we will have s = "abcccd" which compressed is abc3d. Therefore, the optimal way is to delete 'b' and 'd', then the compressed version of s will be "a3c3" of length 4.

**Example 2:**

**Input:** s = "aabbaa", k = 2
**Output:** 2
**Explanation:** If we delete both 'b' characters, the resulting compressed string would be "a4" of length 2.

**Example 3:**

**Input:** s = "aaaaaaaaaaa", k = 0
**Output:** 3
**Explanation:** Since k is zero, we cannot delete anything. The compressed string is "a11" of length 3.

**Constraints:**

- `1 <= s.length <= 100`
- `0 <= k <= s.length`
- `s` contains only lowercase English letters.
### Problem Analysis:
High-level strategy:

- The solution uses a recursive approach with memoization to explore different configurations of compressing and deleting characters to find the optimal compression length.
- The function `count` is the core of the solution, where it computes the optimal compression length for a given set of parameters.

Complexity:

- Time Complexity: O(n * k * n) where n is the length of the input string. This is because for each position in the string, we explore k possible deletions, and at each step, we recursively explore the rest of the string.
- Space Complexity: O(n * k * n) due to the memoization cache.

## Solutions:

```python
class Solution:
    def getLengthOfOptimalCompression(self, s: str, k: int) -> int:
        # Memoization cache to store already computed results
        cache = {}

        # Recursive function to count the optimal compression length
        # i: current index in the string
        # k: remaining deletions allowed
        # prev: previous character
        # prev_count: count of consecutive characters
        def count(i, k, prev, prev_count):
            # Check if the result for the current parameters is already computed
            if (i, k, prev, prev_count) in cache:
                return cache[(i, k, prev, prev_count)]
            
            # If no more deletions are allowed, return infinity
            if k < 0:
                return float("inf")
            
            # If we have reached the end of the string, return 0
            if i == len(s):
                return 0

            # If the current character is the same as the previous one
            if s[i] == prev:
                # Increase the count if it is part of [1, 9, 99] otherwise, keep it the same
                incr = 1 if prev_count in [1, 9, 99] else 0
                # Recursively compute the result for the next character
                res = incr + count(i + 1, k, prev, prev_count + 1)
            else:
                # If we delete the current character, compute the result for the next character with k-1 deletions
                # If we keep the current character, compute the result for the next character with the count reset to 1
                res = min(
                    count(i + 1, k - 1, prev, prev_count),  # delete s[i]
                    1 + count(i + 1, k, s[i], 1)  # don't delete
                )
            
            # Memoize the result and return
            cache[(i, k, prev, prev_count)] = res
            return res

        # Start the recursive function from the beginning of the string with initial parameters
        return count(0, k, "", 0)
```

## Similar Questions