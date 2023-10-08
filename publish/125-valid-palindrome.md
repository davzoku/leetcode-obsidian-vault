---
last_reviewed: 2023-10-08
title: 125 Valid Palindrome - Easy
excerpt: "-"
tags:
  - "#two-pointers"
---
## Problem:
A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**

**Input:** s = "A man, a plan, a canal: Panama"
**Output:** true
**Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**

**Input:** s = "race a car"
**Output:** false
**Explanation:** "raceacar" is not a palindrome.

**Example 3:**

**Input:** s = " "
**Output:** true
**Explanation:** s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.


### Problem Analysis:

- interviewer may not allow us to use built-in functions like `char.isalnum()`, we can implement our own `alnum` by converting the characters to ascii characters
- initialize 2 pointers, one at each side of the side and increment them towards each other and perform a character check using while loop
- take note to move pointer if the current pointer is at a non-alphanumeric character

## Solutions:

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not self.alphaNum(s[l]):
                l +=1
            while r > l and not self.alphaNum(s[r]):
                r -=1
            if s[l].lower() != s[r].lower():
                return False
            l, r = l + 1, r - 1
        return True
    
    def alphaNum(self,c):
        # implement own alphanum func
        # The ord() function returns the number representing the unicode code of a specified character.
        return (ord('A') <= ord(c) <= ord('Z') or
            ord('a') <= ord(c) <= ord('z') or
            ord('0') <= ord(c) <= ord('9'))
```

## Similar Questions