---
last_reviewed: 2024-01-14
title: 1657 - Determine if Two Strings are Close - Medium
excerpt: "-"
tags:
  - solution
  - counting
  - string
  - hashmap
---
## Problem:
Two strings are considered **close** if you can attain one from the other using the following operations:

- Operation 1: Swap any two **existing** characters.
    - For example, `abcde -> aecdb`
- Operation 2: Transform **every** occurrence of one **existing** character into another **existing** character, and do the same with the other character.
    - For example, `aacabb -> bbcbaa` (all `a`'s turn into `b`'s, and all `b`'s turn into `a`'s)

You can use the operations on either string as many times as necessary.

Given two strings, `word1` and `word2`, return `true` _if_ `word1` _and_ `word2` _are **close**, and_ `false` _otherwise._

**Example 1:**

**Input:** word1 = "abc", word2 = "bca"
**Output:** true
**Explanation:** You can attain word2 from word1 in 2 operations.
Apply Operation 1: "abc" -> "acb"
Apply Operation 1: "acb" -> "bca"

**Example 2:**

**Input:** word1 = "a", word2 = "aa"
**Output:** false
**Explanation:** It is impossible to attain word2 from word1, or vice versa, in any number of operations.

**Example 3:**

**Input:** word1 = "cabbba", word2 = "abbccc"
**Output:** true
**Explanation:** You can attain word2 from word1 in 3 operations.
Apply Operation 1: "cabbba" -> "caabbb"
`Apply Operation 2: "`caabbb" -> "baaccc"
Apply Operation 2: "baaccc" -> "abbccc"

**Constraints:**

- `1 <= word1.length, word2.length <= 105`
- `word1` and `word2` contain only lowercase English letters.

### Problem Analysis:
**High-Level Strategy:**

- Calculate the absolute difference in counts for each character using the `Counter` class. This gives us a dictionary with the count differences.
- Sum the absolute differences to get the total steps needed to make the counts of characters in strings `s` and `t` equal.

**Complexity:**

- Time Complexity: O(N + M), where N and M are the lengths of strings `s` and `t`. We iterate through both strings once to create the counts.
- Space Complexity: O(K), where K is the total number of unique characters in both strings. We use additional space to store the counts and differences.

## Solutions:

```python
class Solution:
    def closeStrings(self, word1: str, word2: str) -> bool:
        char1 = Counter(word1)
        char2 = Counter(word2)

        num1 = Counter(char1.values())
        num2 = Counter(char2.values())

        return char1 == char2 or (num1 == num2 and set(word1) == set(word2))
```

## Similar Questions
- [[1347-minimum-number-of-steps-to-make-two-strings-anagram]]