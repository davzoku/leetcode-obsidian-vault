---
last_reviewed: 2023-10-31
title: 20 Valid Parentheses - Easy
excerpt: "-"
tags:
  - solution
  - stack
---
## Problem:
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"
**Output:** true

**Example 2:**

**Input:** s = "()[]{}"
**Output:** true

**Example 3:**

**Input:** s = "(]"
**Output:** false

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.
### Problem Analysis:
- use stack
- O(n) time
## Solutions:

```python
class Solution:
    def isValid(self, s: str) -> bool:
        if not
        stack = []
        closeToOpen = {")":"(", "]": "[", "}":"{"}

        for c in s:
            print(stack)
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return True if not stack else False
```

## Similar Questions