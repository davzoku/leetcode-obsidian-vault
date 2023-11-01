---
last_reviewed: 2023-11-01
title: 1557 Minimum Number of Vertices to Reach All Nodes
excerpt: "-"
tags:
  - solution
  - graph
---
## Problem:

Given a **directed acyclic graph**, with `n` vertices numbered from `0` to `n-1`, and an array `edges` where `edges[i] = [fromi, toi]` represents a directed edge from node `fromi` to node `toi`.

Find _the smallest set of vertices from which all nodes in the graph are reachable_. It's guaranteed that a unique solution exists.

Notice that you can return the vertices in any order.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/07/07/untitled22.png)

**Input:** n = 6, edges = [[0,1],[0,2],[2,5],[3,4],[4,2]]
**Output:** [0,3]
**Explanation:** It's not possible to reach all the nodes from a single vertex. From 0 we can reach [0,1,2,5]. From 3 we can reach [3,4,2,5]. So we output [0,3].

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/07/07/untitled.png)

**Input:** n = 5, edges = [[0,1],[2,1],[3,1],[1,4],[2,4]]
**Output:** [0,2,3]
**Explanation:** Notice that vertices 0, 3 and 2 are not reachable from any other node, so we must include them. Also any of these vertices can reach nodes 1 and 4.

**Constraints:**

- `2 <= n <= 10^5`
- `1 <= edges.length <= min(10^5, n * (n - 1) / 2)`
- `edges[i].length == 2`
- `0 <= fromi, toi < n`
- All pairs `(fromi, toi)` are distinct.

### Problem Analysis:

- simply return a list of nodes with no incoming edges
- O(V+E) time complexity

## Solutions:

```python
class Solution:
    def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
        incoming = collections.defaultdict(list)
        for src, dst in edges:
            incoming[dst].append(src)
        res = []
        for i in range(n):
            if not incoming[i]:
                # get all with no incoming edges
                res.append(i)
        return res
```

## Similar Questions