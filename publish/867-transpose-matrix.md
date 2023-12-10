---
last_reviewed: 2023-12-10
title: 867 Transpose Matrix - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - list-comprehension
---
## Problem:
Given a 2D integer array `matrix`, return _the **transpose** of_ `matrix`.

The **transpose** of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

![](https://assets.leetcode.com/uploads/2021/02/10/hint_transpose.png)

**Example 1:**

**Input:** matrix = [[1,2,3],[4,5,6],[7,8,9]]
**Output:** [[1,4,7],[2,5,8],[3,6,9]]

**Example 2:**

**Input:** matrix = [[1,2,3],[4,5,6]]
**Output:** [[1,4],[2,5],[3,6]]

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 1000`
- `1 <= m * n <= 105`
- `-109 <= matrix[i][j] <= 109`

### Problem Analysis:
- Time Complexity: O(M * N) where M is the number of rows and N is the number of columns
- Space Complexity: O(M * N)

## Solutions:

```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        return [[matrix[j][i] for j in range(len(matrix))] for i in range(len(matrix[0]))]
```

## Similar Questions