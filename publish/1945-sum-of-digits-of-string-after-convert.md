---
last_reviewed: 2024-09-06
title: 1945 Sum of Digits of String After Convert - Easy
excerpt: "-"
tags:
  - solution
  - string
---
## Problem:
You are given a string `s` consisting of lowercase English letters, and an integer `k`.

First, **convert** `s` into an integer by replacing each letter with its position in the alphabet (i.e., replace `'a'` with `1`, `'b'` with `2`, ..., `'z'` with `26`). Then, **transform** the integer by replacing it with the **sum of its digits**. Repeat the **transform** operation `k` **times** in total.

For example, if `s = "zbax"` and `k = 2`, then the resulting integer would be `8` by the following operations:

- **Convert**: `"zbax" ➝ "(26)(2)(1)(24)" ➝ "262124" ➝ 262124`
- **Transform #1**: `262124 ➝ 2 + 6 + 2 + 1 + 2 + 4 ➝ 17`
- **Transform #2**: `17 ➝ 1 + 7 ➝ 8`

Return _the resulting integer after performing the operations described above_.

**Example 1:**

**Input:** s = "iiii", k = 1
**Output:** 36
**Explanation:** The operations are as follows:
- Convert: "iiii" ➝ "(9)(9)(9)(9)" ➝ "9999" ➝ 9999
- Transform #1: 9999 ➝ 9 + 9 + 9 + 9 ➝ 36
Thus the resulting integer is 36.

**Example 2:**

**Input:** s = "leetcode", k = 2
**Output:** 6
**Explanation:** The operations are as follows:
- Convert: "leetcode" ➝ "(12)(5)(5)(20)(3)(15)(4)(5)" ➝ "12552031545" ➝ 12552031545
- Transform #1: 12552031545 ➝ 1 + 2 + 5 + 5 + 2 + 0 + 3 + 1 + 5 + 4 + 5 ➝ 33
- Transform #2: 33 ➝ 3 + 3 ➝ 6
Thus the resulting integer is 6.

**Example 3:**

**Input:** s = "zbax", k = 2
**Output:** 8

**Constraints:**

- `1 <= s.length <= 100`
- `1 <= k <= 10`
- `s` consists of lowercase English letters.

### Problem Analysis:
The solution aims to transform a given string `s` into a numeric value and repeatedly sum the digits of the resultant number for `k` iterations.

- **Step 1:** Convert each character in the string `s` to its corresponding position in the alphabet (where `'a'` = 1, `'b'` = 2, ..., `'z'` = 26). For each character, the numeric position is calculated by `ord(char) - 96`.
- **Step 2:** For each character's position, compute the sum of its digits. This is done by converting the number to a string and then summing its digits.
- **Step 3:** Calculate the sum of all such digit sums for the entire string `s`.
- **Step 4:** Repeat the digit summation process for `k - 1` more iterations on the resultant number from Step 3 to obtain the final result.
- **Time Complexity:**
    - The first loop runs over all characters in `s`, which takes `O(n)`, where `n` is the length of the string `s`.
    - For each character, converting it to its corresponding numeric value and calculating the sum of its digits take `O(1)` time.
    - The second loop iterates `k - 1` times. In each iteration, it calculates the sum of the digits of the number `output`, which takes `O(log(output))` time, where `log(output)` represents the number of digits in `output`.
    - Therefore, the overall time complexity is `O(n + k * log(output))`.
- **Space Complexity:**
    - The space complexity is `O(1)` since only a few integer variables and temporary lists for digit calculations are used, regardless of the input size.

## Solutions:

```python
class Solution:
    def getLucky(self, s: str, k: int) -> int:
        output = 0
        for char in s:
            index = ord(char)-96
            digits = [int(digit) for digit in str(index)]
            result = sum(digits) 
            output += result

        for _ in range(k - 1):
            digits = [int(digit) for digit in str(output)]
            output = sum(digits)
        
        return output
```

## Similar Questions