---
last_reviewed: 2023-12-08
title: 606 Construct String From Binary Tree - Easy
excerpt: "-"
tags:
  - solution
  - binary-tree
  - recursion
---
## Problem:
Given the `root` of a binary tree, construct a string consisting of parenthesis and integers from a binary tree with the preorder traversal way, and return it.

Omit all the empty parenthesis pairs that do not affect the one-to-one mapping relationship between the string and the original binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/03/cons1-tree.jpg)

**Input:** root = [1,2,3,4]
**Output:** "1(2(4))(3)"
**Explanation:** Originally, it needs to be "1(2(4)())(3()())", but you need to omit all the unnecessary empty parenthesis pairs. And it will be "1(2(4))(3)"

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/05/03/cons2-tree.jpg)

**Input:** root = [1,2,3,null,4]
**Output:** "1(2()(4))(3)"
**Explanation:** Almost the same as the first example, except we cannot omit the first parenthesis pair to break the one-to-one mapping relationship between the input and the output.

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-1000 <= Node.val <= 1000`
### Problem Analysis:
- recursively traverse the tree in **preorder** manner
- If logic:
	- if left exists:
		- we want to wrap `left_node.val` with parenthesis
	- if right exists:
		-  we want to wrap `right_node.val` with parenthesis
	- if left don't exist but right exists (Edge case, case 2):
		- we want an empty parenthesis as placeholder for left node
		- we want to wrap `right_node.val` with parenthesis
- Simplifying the logic, we just need:
	- `if left_str or right_str:`
	- `if right_str:`

- **Time Complexity:**
    - The time complexity remains O(n), where n is the number of nodes in the binary tree, as each node is visited once.
    
- **Space Complexity:**
    - The space complexity is O(h), where h is the height of the binary tree, due to the recursive call stack.


## Solutions:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def tree2str(self, root: Optional[TreeNode]) -> str:
        if not root:
            return ""

        left_str = self.tree2str(root.left)
        right_str = self.tree2str(root.right)

        result = str(root.val)

        if left_str or right_str:
            result += "(" + left_str + ")"

        if right_str:
            result += "(" + right_str + ")"

        return result
```

## Similar Questions