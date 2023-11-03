---
last_reviewed: 2023-11-03
title: 
excerpt: "-"
tags:
  - solution
  - graph
---
## Problem:
You are given a list of bombs. The **range** of a bomb is defined as the area where its effect can be felt. This area is in the shape of a **circle** with the center as the location of the bomb.

The bombs are represented by a **0-indexed** 2D integer array `bombs` where `bombs[i] = [xi, yi, ri]`. `xi` and `yi` denote the X-coordinate and Y-coordinate of the location of the `ith` bomb, whereas `ri` denotes the **radius** of its range.

You may choose to detonate a **single** bomb. When a bomb is detonated, it will detonate **all bombs** that lie in its range. These bombs will further detonate the bombs that lie in their ranges.

Given the list of `bombs`, return _the **maximum** number of bombs that can be detonated if you are allowed to detonate **only one** bomb_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/11/06/desmos-eg-3.png)

**Input:** bombs = [[2,1,3],[6,1,4]]
**Output:** 2
**Explanation:**
The above figure shows the positions and ranges of the 2 bombs.
If we detonate the left bomb, the right bomb will not be affected.
But if we detonate the right bomb, both bombs will be detonated.
So the maximum bombs that can be detonated is max(1, 2) = 2.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/11/06/desmos-eg-2.png)

**Input:** bombs = [[1,1,5],[10,10,5]]
**Output:** 1
**Explanation:**
Detonating either bomb will not detonate the other bomb, so the maximum number of bombs that can be detonated is 1.

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/11/07/desmos-eg1.png)

**Input:** bombs = [[1,2,3],[2,3,1],[3,4,2],[4,5,3],[5,6,4]]
**Output:** 5
**Explanation:**
The best bomb to detonate is bomb 0 because:
- Bomb 0 detonates bombs 1 and 2. The red circle denotes the range of bomb 0.
- Bomb 2 detonates bomb 3. The blue circle denotes the range of bomb 2.
- Bomb 3 detonates bomb 4. The green circle denotes the range of bomb 3.
Thus all 5 bombs are detonated.

**Constraints:**

- `1 <= bombs.length <= 100`
- `bombs[i].length == 3`
- `1 <= xi, yi, ri <= 105`

### Problem Analysis:
- build directed adjacency list for each bomb (node), and run dfs
- O(n^3) time complexity
- O(n^2) space complexity

## Solutions:

```python
class Solution:
    def maximumDetonation(self, bombs: List[List[int]]) -> int:
        adj = collections.defaultdict(list) # bomb -> [list of bombs]

        for i in range(len(bombs)):
            for j in range(i+1, len(bombs)):
                x1,y1, r1 = bombs[i]
                x2,y2, r2 = bombs[j]
                d = sqrt((x1- x2)**2 + (y1-y2)**2)

                if d <= r1:
                    adj[i].append(j)
                if d <= r2:
                    adj[j].append(i)

        def dfs(i, visit):
            if i in visit:
                return 0
            visit.add(i)
            for nei in adj[i]:
                dfs(nei, visit)
            return len(visit)
        res = 0
        for i in range(len(bombs)):
            res = max(res, dfs(i, set()))
        return res
```

## Similar Questions