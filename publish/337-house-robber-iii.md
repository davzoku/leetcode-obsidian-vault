---
last_reviewed: 2023-10-09
title: 337 House Robber - Medium
excerpt: "-"
tags:
  - "#binary-tree"
  - solution
---
## Problem:
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if **two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return _the maximum amount of money the thief can rob **without alerting the police**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg)

**Input:** root = [3,2,3,null,3,null,1]
**Output:** 7
**Explanation:** Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/10/rob2-tree.jpg)

**Input:** root = [3,4,5,1,3,null,1]
**Output:** 9
**Explanation:** Maximum amount of money the thief can rob = 4 + 5 = 9.

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `0 <= Node.val <= 104`

### Problem Analysis:

- modify dfs to return 2 values instead of 1
- then get max between withRoot and withoutRoot

## Solutions:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:
        return max(self.dfs(root))
    
    def dfs(self, root: Optional[TreeNode]) -> [int, int]:
        if not root:
	        # withoutRoot, withRoot
            return [0, 0]
        
        leftPair = self.dfs(root.left)
        rightPair = self.dfs(root.right)
        # get element 1 to get without 
        withRoot = root.val + leftPair[1] + rightPair[1]
        withoutRoot = max(leftPair) + max(rightPair)

        return [withRoot, withoutRoot]

```

## Similar Questions

- [[198-house-robber]]
- [[213-house-robber-ii]]
- [[2560-house-robber-iv]]