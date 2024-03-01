---
last_reviewed: 2024-03-01
title: 2864 Maximum Odd Binary Number - Easy
excerpt: "-"
tags:
  - solution
  - math
  - string
---
## Problem:
You are given a **binary** string `s` that contains at least one `'1'`.

You have to **rearrange** the bits in such a way that the resulting binary number is the **maximum odd binary number** that can be created from this combination.

Return _a string representing the maximum odd binary number that can be created from the given combination._

**Note** that the resulting string **can** have leading zeros.

**Example 1:**

**Input:** s = "010"
**Output:** "001"
**Explanation:** Because there is just one '1', it must be in the last position. So the answer is "001".

**Example 2:**

**Input:** s = "0101"
**Output:** "1001"
**Explanation:** One of the '1's must be in the last position. The maximum number that can be made with the remaining digits is "100". So the answer is "1001".

**Constraints:**

- `1 <= s.length <= 100`
- `s` consists only of `'0'` and `'1'`.
- `s` contains at least one `'1'`.

### Problem Analysis:
1. **High-Level Strategy**:
    
    - The function aims to find the maximum odd binary number that can be formed by rearranging the digits of the given binary string `s`.
    - The strategy here involves finding the rightmost '1' in the string and moving all other '1's to the far left.
    - After moving all '1's except the rightmost one, append a '1' to the end of the string to make it an odd number.
2. **Complexity Analysis**:
    
    - Finding the rightmost '1' in a string using `rfind()` takes O(n) time, where n is the length of the string `s`.
    - Counting the occurrences of '1' in the string using `count()` takes O(n) time as well.
    - Constructing the result string involves concatenating strings which takes O(n) time, where n is the length of the string `s`.
    - Overall, the time complexity of the solution is O(n), where n is the length of the input string `s`. The space complexity is also O(n) due to the space required to store the result string.

## Solutions:

```python
class Solution:
    def maximumOddBinaryNumber(self, s: str) -> str:
        # Find the rightmost '1'
        idx = s.rfind('1')
        # Move all '1's except the rightmost one to the far left
        result = '1' * (s.count('1') - 1) + '0' * (len(s) - s.count('1'))
        # Add the rightmost '1' to the end
        result += '1'
        return result
```

## Similar Questions