---
last_reviewed: 2023-12-30
title: 1897 Redistribute Characters to Make All Strings Equal - Easy
excerpt: "-"
tags:
  - solution
  - hashmap
  - string
  - counting
---
## Problem:
You are given an array of strings `words` (**0-indexed**).

In one operation, pick two **distinct** indices `i` and `j`, where `words[i]` is a non-empty string, and move **any** character from `words[i]` to **any** position in `words[j]`.

Return `true` _if you can make **every** string in_ `words` _**equal** using **any** number of operations_, _and_ `false` _otherwise_.

**Example 1:**

**Input:** words = ["abc","aabc","bc"]
**Output:** true
**Explanation:** Move the first 'a' in `words[1] to the front of words[2], to make` `words[1]` = "abc" and words[2] = "abc".
All the strings are now equal to "abc", so return `true`.

**Example 2:**

**Input:** words = ["ab","a"]
**Output:** false
**Explanation:** It is impossible to make all the strings equal using the operation.

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists of lowercase English letters.

### Problem Analysis:

High-level strategy:

- The solution uses a Counter to count the occurrences of each character in all words.
- It then checks if the count of each character is divisible by the total number of words. If any character count is not divisible, it returns False. Otherwise, it returns True.

Complexity:

- Time Complexity: O(C), where C is the total number of characters across all words. The solution iterates through all characters in all words once.
- Space Complexity: O(C), where C is the total number of characters across all words. The Counter keeps track of character counts.

## Solutions:

```python
class Solution:
    def makeEqual(self, words: List[str]) -> bool:
        counts = Counter()

        for word in words:
            counts.update(word)

        for count in counts.values():
            if count % len(words) != 0:
                return False

        return True
```

## Similar Questions