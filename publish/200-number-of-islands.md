---
last_reviewed: 2023-10-13
title: 200 Number of Islands - Medium
excerpt: "-"
tags:
  - graph
  - breadth-first-search
---
## Problem:

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
**Output:** 1

**Example 2:**

**Input:** grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
**Output:** 3

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

### Problem Analysis:

- can use both BFS and DFS
- for each cell in the grid
	- if land is found and not visited
	- do a BFS to find all connecting land 
	- increment island coun
- define a bfs helper function to explore the grid space

## Solutions:

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        # used bfs, can also change to dfs

        # base case
        if not grid:
            return 0
        
        rows, cols = len(grid), len(grid[0])
        visited = set()
        islands = 0

        def bfs(r, c):
            q = collections.deque()
            visited.add((r,c))
            q.append((r,c))

            while q: 
                row, col = q.popleft()
                # right left up down
                directions = [[1,0], [-1, 0], [0,1], [0,-1]]
                for dr, dc in directions:
                    r, c = row + dr, col + dc
                    if (r in range(rows) and
                        c in range(cols) and
                        grid[r][c] == "1" and 
                        (r,c) not in visited):                

                        q.append((r,c))
                        visited.add((r,c))        

        for r in range(rows):
            for c in range(cols):
                # if found another land and not visited, increment island count
                if grid[r][c] == "1" and (r,c) not in visited:
                    bfs(r,c)
                    islands +=1

        return islands
```

## Similar Questions