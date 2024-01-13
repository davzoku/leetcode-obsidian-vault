---
last_reviewed: 2024-01-13
title: 1347 Minimum Number of Steps to Make Two Strings Anagram - Medium
excerpt: "-"
tags:
  - solution
---
## Problem:
You are given two strings of the same length `s` and `t`. In one step you can choose **any character** of `t` and replace it with **another character**.

Return _the minimum number of steps_ to make `t` an anagram of `s`.

An **Anagram** of a string is a string that contains the same characters with a different (or the same) ordering.

**Example 1:**

**Input:** s = "bab", t = "aba"
**Output:** 1
**Explanation:** Replace the first 'a' in t with b, t = "bba" which is anagram of s.

**Example 2:**

**Input:** s = "leetcode", t = "practice"
**Output:** 5
**Explanation:** Replace 'p', 'r', 'a', 'i' and 'c' from t with proper characters to make t anagram of s.

**Example 3:**

**Input:** s = "anagram", t = "mangaar"
**Output:** 0
**Explanation:** "anagram" and "mangaar" are anagrams. 

**Constraints:**

- `1 <= s.length <= 5 * 104`
- `s.length == t.length`
- `s` and `t` consist of lowercase English letters only.

### Problem Analysis:
**High-Level Strategy:**

- We use the `Counter` class to count the occurrences of each character in strings `s` and `t`.
- For each unique character in both strings, we calculate the absolute difference in counts.
- The total steps needed to make the counts equal is the sum of these differences.
- We divide the total steps by 2, as each difference corresponds to both a removal in `s` and an addition in `t`.

**Complexity:**

- Time Complexity: O(N + M), where N and M are the lengths of strings `s` and `t`. We iterate through both strings once to create the counts.
- Space Complexity: O(K), where K is the total number of unique characters in both strings. We use additional space to store the counts and keys.

## Solutions:

```python
class Solution:
    def minSteps(self, s: str, t: str) -> int:
        count_s = Counter(s)
        count_t = Counter(t)
        # x = set(count_s.keys())
        # y = set(count_t.keys())

        # all_keys = x.union(y)
        all_keys = count_s.keys() | count_t.keys()

        # Calculate the absolute difference in counts for each key
        differences = sum(abs(count_s.get(key, 0) - count_t.get(key, 0)) for key in all_keys)

        return differences//2 
```

Alternatively, we can do it in 1 line

```python
class Solution:
    def minSteps(self, s: str, t: str) -> int:
        return sum(list((Counter(t)-Counter(s)).values()))
```
## Similar Questions