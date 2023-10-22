---
last_reviewed: 2023-10-22
title: 617 Merge Two Binary Tree - Easy
excerpt: "-"
tags:
  - solution
  - binary-tree
---
## Problem:

You are given two binary trees `root1` and `root2`.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return _the merged tree_.

**Note:** The merging process must start from the root nodes of both trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/05/merge.jpg)

**Input:** root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
**Output:** [3,4,5,5,4,null,7]

**Example 2:**

**Input:** root1 = [1], root2 = [1,2]
**Output:** [2,2]

**Constraints:**

- The number of nodes in both trees is in the range `[0, 2000]`.
- `-104 <= Node.val <= 104`

### Problem Analysis:

- recursive approach

## Solutions:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1:
            return root2
        if not root2:
            return root1

        tree = TreeNode(root1.val + root2.val)
        tree.left = self.mergeTrees(root1.left, root2.left)
        tree.right = self.mergeTrees(root1.right, root2.right)

        return tree
```

## Similar Questions