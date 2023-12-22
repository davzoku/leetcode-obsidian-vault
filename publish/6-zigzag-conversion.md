---
last_reviewed: 2023-12-22
title: 6 Zigzag Conversion - Medium
excerpt: "-"
tags:
  - solution
  - string
---
## Problem:
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);

**Example 1:**

**Input:** s = "PAYPALISHIRING", numRows = 3
**Output:** "PAHNAPLSIIGYIR"

**Example 2:**

**Input:** s = "PAYPALISHIRING", numRows = 4
**Output:** "PINALSIGYAHRPI"
**Explanation:**
P     I    N
A   L S  I G
Y A   H R
P     I

**Example 3:**

**Input:** s = "A", numRows = 1
**Output:** "A"

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
- `1 <= numRows <= 1000`

### Problem Analysis:
### Solution 1:

#### High-Level Strategy:

- Creates a list `rows` of size `numRows` to store characters for each row.
- Iterates through each character in the input string `s`.
- Appends each character to the corresponding row in `rows` based on the zigzag pattern.
- Manages the zigzag pattern using the `index` and `step` variables.

#### Complexity:

- **Time Complexity:** O(N), where N is the length of the input string `s`. Each character is processed once.
- **Space Complexity:** O(N), the space used by the list `rows`.

### Solution 2:
_diagram from [Neetcode](https://www.youtube.com/watch?v=Q2Tw6gcVEwc)_
![[6-1.png]]

#### High-Level Strategy:

- Uses a list `res_rows` to store characters for each row.
- Iterates through each character in the input string `s` using `enumerate`.
- Calculates the row number based on the zigzag pattern and appends the character to the corresponding row in `res_rows`.
- Concatenates the rows into a single string at the end.

#### Complexity:

- **Time Complexity:** O(N), where N is the length of the input string `s`. Each character is processed once.
- **Space Complexity:** O(N), the space used by the list `res_rows`.

### Comparison:

- Both solutions have the same time complexity, but solution 2 avoids unnecessary checks and calculations within the loop.
- Solution 2 is more concise and straightforward in handling the zigzag pattern. However, you need to figure out the underlying formula.

## Solutions:
### Solution 1:

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1 or numRows >= len(s):
            return s

        rows = [''] * numRows
        index, step = 0, 1

        for char in s:
            rows[index] += char
            if index == 0:
                step = 1
            elif index == numRows - 1:
	            # turning pt of zigzag
                step = -1
            index += step

        return ''.join(rows)
```

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        
        res_rows = [''] * numRows

        for i, char in enumerate(s):
            remainder = i % (2 * (numRows - 1))
            row = numRows - 1 - abs(numRows - 1 - remainder)
            res_rows[row] += char

        return ''.join(res_rows)
```
## Similar Questions