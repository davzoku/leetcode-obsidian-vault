---
last_reviewed: 2023-12-02
title: 1160 Find Words That Can Be Formed By Characters - Easy
excerpt: "-"
tags:
  - solution
  - hashmap
---
## Problem:
You are given an array of strings `words` and a string `chars`.

A string is **good** if it can be formed by characters from chars (each character can only be used once).

Return _the sum of lengths of all good strings in words_.

**Example 1:**

**Input:** words = ["cat","bt","hat","tree"], chars = "atach"
**Output:** 6
**Explanation:** The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.

**Example 2:**

**Input:** words = ["hello","world","leetcode"], chars = "welldonehoneyr"
**Output:** 10
**Explanation:** The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.

**Constraints:**

- `1 <= words.length <= 1000`
- `1 <= words[i].length, chars.length <= 100`
- `words[i]` and `chars` consist of lowercase English letters.

### Problem Analysis:
- Create a hashmap (`count`) to store the count of each character in the `chars` string.
- Iterate through a nested loop for each word in the list of words and each character in each word:
    - Check if the character exists in the `count` hashmap.
    - Verify that the count of the character in the current word is less than or equal to its count in the hashmap.
- Sum the lengths of all "good" words to obtain the final output.

**Time Complexity:**
- O(N * K + M), where N is the average length of words in the list `words`, K is the number of words in `words`, and M is the length of the `chars` string.

**Space Complexity:**
- O(N + M), where N represents the space required for the hashmap (`count`), and M is the size of the character set in `chars`.

## Solutions:

```python
class Solution:
    def countCharacters(self, words: List[str], chars: str) -> int:
        count = Counter(chars)
        res = 0
        

        for word in words:
            cur_word = defaultdict(int)

            good = True
            for char in word:
                cur_word[char] += 1
                if char not in count or cur_word[char] > count[char]:
                    # char dont exist or 
                    # curr word has more char than the counter
                    good = False
                    break
            if good:
                res += len(word)

        return res
```

## Similar Questions