---
last_reviewed: 2023-12-09
title: 94 Binary Tree Inorder Traversal - Easy
excerpt: "-"
tags:
  - solution
  - recursion
  - iterative
  - binary-tree
---
## Problem:
Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

**Input:** root = [1,null,2,3]
**Output:** [1,3,2]

**Example 2:**

**Input:** root = []
**Output:** []

**Example 3:**

**Input:** root = [1]
**Output:** [1]

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

**Follow up:** Recursive solution is trivial, could you do it iteratively?

### Problem Analysis:
- Time Complexity: O(N) where N is the number of nodes
- Space Complexity: O(H) where H is the height of the binary tree

## Solutions:

### Recursion

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        self.inorder_recur(root, result)
        return result
    
    def inorder_recur(self, node, result):
        if node:
            # Traverse left subtree
            self.inorder_recur(node.left, result)
            
            # Visit the root node
            result.append(node.val)
            
            # Traverse right subtree
            self.inorder_recur(node.right, result)
```

### Iterative
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        stack = []
        current = root

        while current or stack:
            # Traverse as left as possible, pushing nodes onto the stack
            while current:
                stack.append(current)
                current = current.left

            current = stack.pop()
            result.append(current.val)
            # Move to the right child of the popped node
            current = current.right

        return result```
## Similar Questions