---
last_reviewed: 2023-12-13
title: 1582 Special Positions in a Binary Matrix - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - matrix
---
## Problem:
Given an `m x n` binary matrix `mat`, return _the number of special positions in_ `mat`_._

A position `(i, j)` is called **special** if `mat[i][j] == 1` and all other elements in row `i` and column `j` are `0` (rows and columns are **0-indexed**).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/12/23/special1.jpg)

**Input:** mat = [[1,0,0],[0,0,1],[1,0,0]]
**Output:** 1
**Explanation:** (1, 2) is a special position because mat[1][2] == 1 and all other elements in row 1 and column 2 are 0.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/12/24/special-grid.jpg)

**Input:** mat = [[1,0,0],[0,1,0],[0,0,1]]
**Output:** 3
**Explanation:** (0, 0), (1, 1) and (2, 2) are special positions.

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 100`
- `mat[i][j]` is either `0` or `1`.

### Problem Analysis:
1. **Initialization**: `row_ones` and `col_ones` are initialized to store the count of ones in each row and column, respectively.
    
2. **Counting Ones**: The first loop iterates through the matrix, counting the number of ones in each row (`row_ones`) and each column (`col_ones`).
    
3. **Checking Special Positions**: The second loop iterates through the matrix again and checks if a cell has a value of 1 (`nums[i][j] == 1`) and if it's the only one in its row (`row_ones[i] == 1`) and the only one in its column (`col_ones[j] == 1`). If all conditions are met, `result` is incremented.
    

**Time Complexity:** The time complexity of the code is O(rows * cols) because there are two nested loops that iterate through the entire matrix.

**Space Complexity:** The space complexity is O(rows + cols) as we use two additional lists (`row_ones` and `col_ones`) to store counts for each row and column.

## Solutions:

```python
class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        result = 0
        rows, cols = len(mat), len(mat[0])
        row_ones = [0] * rows
        col_ones = [0] * cols

        # count 1s in rows and cols
        for i in range(rows):
            for j in range(cols):
                if mat[i][j] == 1:
                    row_ones[i] += 1
                    col_ones[j] += 1

        # check and increment
        for i in range(rows):
            for j in range(cols):
                if mat[i][j] == 1 and row_ones[i] == 1 and col_ones[j] == 1:
                    result += 1

        return result        
```

## Similar Questions