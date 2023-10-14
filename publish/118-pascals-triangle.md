---
last_reviewed: 2023-10-15
title: 118 Pascal's Triangle - Easy
excerpt: "-"
tags:
  - solution
  - dynamic-programming
---
## Problem:

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

**Input:** numRows = 5
**Output:** [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

**Example 2:**

**Input:** numRows = 1
**Output:** [[1]]

**Constraints:**

- `1 <= numRows <= 30`

### Problem Analysis:

- dynamic programming
- **Trick**: add zero at the side

## Solutions:

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        res = [[1]]

        for i in range(numRows - 1):
            # previous row, add 0 at the side for easy calculation
            temp = [0] + res[-1] + [0]
            row = []
            for j in range(len(res[-1])+1):
                row.append(temp[j] + temp[j+1])
            res.append(row)

        return res
```

## Similar Questions