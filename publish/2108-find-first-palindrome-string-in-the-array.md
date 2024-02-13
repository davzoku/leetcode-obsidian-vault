---
last_reviewed: 2024-02-13
title: "2108"
excerpt: "-"
tags:
  - solution
  - two-pointers
  - string
  - arrays
---
## Problem:
Given an array of strings `words`, return _the first **palindromic** string in the array_. If there is no such string, return _an **empty string**_ `""`.

A string is **palindromic** if it reads the same forward and backward.

**Example 1:**

**Input:** words = ["abc","car","ada","racecar","cool"]
**Output:** "ada"
**Explanation:** The first string that is palindromic is "ada".
Note that "racecar" is also palindromic, but it is not the first.

**Example 2:**

**Input:** words = ["notapalindrome","racecar"]
**Output:** "racecar"
**Explanation:** The first and only string that is palindromic is "racecar".

**Example 3:**

**Input:** words = ["def","ghi"]
**Output:** ""
**Explanation:** There are no palindromic strings, so the empty string is returned.

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists only of lowercase English letters.

### Problem Analysis:
1. **High-Level Strategy**:
    
    - The solution iterates through each word in the given list.
    - For each word, it checks if the word is equal to its reverse (`i == i[::-1]`).
    - If a palindrome is found, it returns that word.
    - If no palindrome is found after iterating through all words, it returns an empty string.
2. **Complexity**:
    
    - Let's denote n as the number of words in the input list and m as the average length of the words.
    - Iterating through each word in the list takes O(n) time.
    - Checking if a word is a palindrome by comparing it with its reverse (`i == i[::-1]`) takes O(m) time.
    - Overall, the time complexity of this solution is O(n⋅m).
    - There is no additional space complexity incurred by the algorithm apart from the input and output, so the space complexity is O(1) (constant space).

## Solutions:

```python
class Solution:
    def firstPalindrome(self, words: List[str]) -> str:
        for i in words:
            if i == i[::-1]:
                return i
        return ""
```

## Similar Questions
- [[125-valid-palindrome]]