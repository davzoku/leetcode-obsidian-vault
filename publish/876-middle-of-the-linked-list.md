---
last_reviewed: 2024-03-07
title: 876 Middle of the Linked List - Easy
excerpt: "-"
tags:
  - solution
  - linked-list
  - two-pointers
  - tortoise-and-hare
---
## Problem:
Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [3,4,5]
**Explanation:** The middle node of the list is node 3.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

**Input:** head = [1,2,3,4,5,6]
**Output:** [4,5,6]
**Explanation:** Since the list has two middle nodes with values 3 and 4, we return the second one.

**Constraints:**

- The number of nodes in the list is in the range `[1, 100]`.
- `1 <= Node.val <= 100`

### Problem Analysis:
### 1. High Level Strategy:

The solution employs the concept of slow and fast pointers to find the middle node of the linked list. Initially, both pointers, `slow` and `fast`, are set to the head of the linked list. The `slow` pointer moves one node at a time, while the `fast` pointer moves two nodes at a time. By the time the `fast` pointer reaches the end of the list, the `slow` pointer will be at the middle node. This is due to the relative speeds of the two pointers - the `fast` pointer moves twice as fast as the `slow` pointer, so when the `fast` pointer reaches the end, the `slow` pointer will be at the midpoint.

### 2. Complexity:

- Time Complexity: The algorithm traverses the linked list once, with the `fast` pointer moving twice as fast as the `slow` pointer. Hence, the time complexity is O(n), where n is the number of nodes in the linked list.
- Space Complexity: The algorithm uses only a constant amount of extra space for two pointers (`slow` and `fast`), regardless of the size of the input linked list. Thus, the space complexity is O(1).

## Solutions:

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        return slow
```

## Similar Questions