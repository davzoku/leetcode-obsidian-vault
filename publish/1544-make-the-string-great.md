---
last_reviewed: 2024-04-05
title: 1544 Make The String Great - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
Given a string `s` of lower and upper case English letters.

A good string is a string which doesn't have **two adjacent characters** `s[i]` and `s[i + 1]` where:

- `0 <= i <= s.length - 2`
- `s[i]` is a lower-case letter and `s[i + 1]` is the same letter but in upper-case or **vice-versa**.

To make the string good, you can choose **two adjacent** characters that make the string bad and remove them. You can keep doing this until the string becomes good.

Return _the string_ after making it good. The answer is guaranteed to be unique under the given constraints.

**Notice** that an empty string is also good.

**Example 1:**

**Input:** s = "leEeetcode"
**Output:** "leetcode"
**Explanation:** In the first step, either you choose i = 1 or i = 2, both will result "leEeetcode" to be reduced to "leetcode".

**Example 2:**

**Input:** s = "abBAcC"
**Output:** ""
**Explanation:** We have many possible scenarios, and all lead to the same answer. For example:
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""

**Example 3:**

**Input:** s = "s"
**Output:** "s"

**Constraints:**

- `1 <= s.length <= 100`
- `s` contains only lower and upper case English letters.

### Problem Analysis:
1. **High-Level Strategy:**
    - The solution utilizes a stack data structure to handle the removal of adjacent characters of opposite cases.
    - It iterates through the given string `s`, checking each character.
    - If the stack is not empty, it checks if the current character and the last character in the stack are of opposite cases (upper and lower or vice versa). If they are, it pops the last character from the stack (which effectively removes both adjacent characters) and continues to the next character.
    - If the characters are not of opposite cases, it simply appends the current character to the stack.
    - Finally, it joins the characters remaining in the stack and returns the resulting string.
2. **Complexity:**
    - Time Complexity: The time complexity of this solution is O(n), where n is the length of the input string `s`. This is because the solution iterates through each character of the string once.
    - Space Complexity: The space complexity is also O(n), where n is the length of the input string `s`. This is because the stack can contain at most all characters of the string if none of them are removed. However, in the worst-case scenario, where all characters are removed alternately, the stack would only contain half of the characters. Therefore, the space complexity is linear with respect to the input size.

## Solutions:

```python
class Solution:
    def makeGood(self, s: str) -> str:
        stack = []
        
        for char in s:
            if stack:
                # Check if the last character in the stack is of opposite case
                if (char.islower() and stack[-1] == char.upper()) or (char.isupper() and stack[-1] == char.lower()):
                    stack.pop()  # Remove the last character if it is of opposite case
                    continue
            stack.append(char)
        
        return ''.join(stack)
```

## Similar Questions