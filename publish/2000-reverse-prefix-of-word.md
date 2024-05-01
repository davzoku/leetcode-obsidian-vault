---
last_reviewed: 2024-05-01
title: 2000 Reverse Prefix of Word - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
Given a **0-indexed** string `word` and a character `ch`, **reverse** the segment of `word` that starts at index `0` and ends at the index of the **first occurrence** of `ch` (**inclusive**). If the character `ch` does not exist in `word`, do nothing.

- For example, if `word = "abcdefd"` and `ch = "d"`, then you should **reverse** the segment that starts at `0` and ends at `3` (**inclusive**). The resulting string will be `"dcbaefd"`.

Return _the resulting string_.

**Example 1:**

**Input:** word = "abcdefd", ch = "d"
**Output:** "dcbaefd"
**Explanation:** The first occurrence of "d" is at index 3. 
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "dcbaefd".

**Example 2:**

**Input:** word = "xyxzxe", ch = "z"
**Output:** "zxyxxe"
**Explanation:** The first and only occurrence of "z" is at index 3.
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "zxyxxe".

**Example 3:**

**Input:** word = "abcd", ch = "z"
**Output:** "abcd"
**Explanation:** "z" does not exist in word.
You should not do any reverse operation, the resulting string is "abcd".

**Constraints:**

- `1 <= word.length <= 250`
- `word` consists of lowercase English letters.
- `ch` is a lowercase English letter.

### Problem Analysis:
1. **High-level strategy**:
    
    - The solution iterates through each character in the word until it finds the target character `ch`.
    - Once found, it stores the index of `ch`.
    - It then reverses the substring from the beginning of the word up to and including the index of `ch`.
    - Finally, it concatenates the reversed prefix with the remaining part of the word.
2. **Complexity**:
    
    - Time Complexity:
        - The loop iterates through the entire word, which takes O(n) time, where n is the length of the word.
        - Reversing the prefix takes O(m) time, where m is the length of the prefix (up to `ch`).
        - Concatenation takes O(n-m) time, as it only involves the remaining part of the word.
        - Overall, the time complexity is O(n).
    - Space Complexity:
        - The solution doesn't use any extra space proportional to the input size, apart from the output variable.
        - The space complexity is O(1), constant space.

## Solutions:

```python
class Solution:
    def reversePrefix(self, word: str, ch: str) -> str:
        index = None
        for i, w in enumerate(word):
            if w == ch:
                index = i
                break
        output = word
        if index:
            output = f"{word[:index+1][::-1]}{word[index+1:]}"
        return output
```

## Similar Questions