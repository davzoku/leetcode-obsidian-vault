---
last_reviewed: 2023-10-26
title: 119 Pascal's Triangle II - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:

Given an integer `rowIndex`, return the `rowIndexth` (**0-indexed**) row of the **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

**Input:** rowIndex = 3
**Output:** [1,3,3,1]

**Example 2:**

**Input:** rowIndex = 0
**Output:** [1]

**Example 3:**

**Input:** rowIndex = 1
**Output:** [1,1]

**Constraints:**

- `0 <= rowIndex <= 33`

**Follow up:** Could you optimize your algorithm to use only `O(rowIndex)` extra space?

### Problem Analysis:

- slight modification from [[118-pascals-triangle]]

## Solutions:

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        res = [[1]]

        for i in range(rowIndex):
            # previous row, add 0 at the side for easy calculation
            temp = [0] + res[-1] + [0]
            row = []
            for j in range(len(res[-1])+1):
                row.append(temp[j] + temp[j+1])
            res.append(row)

        return res[-1]      
```

## Similar Questions
[[118-pascals-triangle]]