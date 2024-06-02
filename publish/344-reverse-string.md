---
last_reviewed: 2024-06-02
title: 344 Reverse String - Easy
excerpt: "-"
tags:
  - solution
  - string
  - two-pointers
---
## Problem:
Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

**Example 1:**

**Input:** s = ["h","e","l","l","o"]
**Output:** ["o","l","l","e","h"]

**Example 2:**

**Input:** s = ["H","a","n","n","a","h"]
**Output:** ["h","a","n","n","a","H"]

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is a [printable ascii character](https://en.wikipedia.org/wiki/ASCII#Printable_characters).
### Problem Analysis:
1. **High-level strategy**:
   - The solution employs slicing to reverse the list `s` in place.
   - By using the syntax `s[:]`, it modifies the original list `s` instead of creating a new one.
   - `s[::-1]` creates a reversed copy of the list, and then `s[:]` assigns this reversed copy back to the original list, effectively reversing it in place.

2. **Complexity**:
   - Time Complexity: 
     - Reversing the list using slicing `s[::-1]` takes O(n), where n is the length of the list `s`.
     - Assigning the reversed list back to `s` using slicing `s[:] = ...` also takes O(n), as it iterates through all elements of the list.
     - Therefore, the overall time complexity is O(n).
   - Space Complexity: 
     - The space complexity is O(1) because the solution modifies the input list in place, without using any additional space proportional to the input size. However, technically, slicing creates a new list, but since it's not stored separately and the original list is modified directly, the space complexity is considered constant, O(1).


## Solutions:

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        s[:] = s[::-1]
```

## Similar Questions