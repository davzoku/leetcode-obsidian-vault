---
last_reviewed: 2024-01-12
title: 1704 Determine if String Halves Are Alike - Easy
excerpt: "-"
tags:
  - solution
  - string
  - counting
---
## Problem:
You are given a string `s` of even length. Split this string into two halves of equal lengths, and let `a` be the first half and `b` be the second half.

Two strings are **alike** if they have the same number of vowels (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`, `'A'`, `'E'`, `'I'`, `'O'`, `'U'`). Notice that `s` contains uppercase and lowercase letters.

Return `true` _if_ `a` _and_ `b` _are **alike**_. Otherwise, return `false`.

**Example 1:**

**Input:** s = "book"
**Output:** true
**Explanation:** a = "bo" and b = "ok". a has 1 vowel and b has 1 vowel. Therefore, they are alike.

**Example 2:**

**Input:** s = "textbook"
**Output:** false
**Explanation:** a = "text" and b = "book". a has 1 vowel whereas b has 2. Therefore, they are not alike.
Notice that the vowel o is counted twice.

**Constraints:**

- `2 <= s.length <= 1000`
- `s.length` is even.
- `s` consists of **uppercase and lowercase** letters.

### Problem Analysis
**High-Level Strategy:**

1. **Initialization:** Initialize a string `vowels` with the vowels "aeiou". Convert the input string `s` to lowercase to make the comparison case-insensitive.
    
2. **Check Length:** If the length of the string `s` is odd, return `False` because the string cannot be split into equal halves.
    
3. **Calculate Midpoint:** Calculate the midpoint of the string `s` by using integer division (`length // 2`).
    
4. **Count Vowels in Halves:** Count the number of vowels in the first half (`s[:mid]`) and the second half (`s[mid:]`) using a generator expression and the `sum` function.
    
5. **Comparison:** Return `True` if the counts of vowels in the first half are equal to the counts in the second half; otherwise, return `False`.
    

**Complexity:**

- **Time Complexity:** The time complexity is O(N), where N is the length of the input string `s`. The algorithm iterates through the string once to calculate the counts of vowels in the first and second halves.
    
- **Space Complexity:** The space complexity is O(1). The algorithm uses a constant amount of space for the `vowels` string and a few variables (`length`, `mid`, `count_first`, `count_second`). The space required does not grow with the input size.

## Solutions:

```python
class Solution:
    def halvesAreAlike(self, s: str) -> bool:
        vowels = "aeiou"
        s = s.lower()
        length = len(s)
        if length % 2 == 1:
            return False

        mid = length // 2
        count_first = sum(1 for char in s[:mid] if char in vowels)
        count_second = sum(1 for char in s[mid:] if char in vowels)


        return count_first == count_second
```

## Similar Questions