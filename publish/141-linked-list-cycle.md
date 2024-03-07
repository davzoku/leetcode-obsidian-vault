---
last_reviewed: 2024-03-06
title: 141 Linked List Cycle - Easy
excerpt: "-"
tags:
  - solution
  - two-pointers
  - linked-list
  - tortoise-and-hare
---
## Problem:
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Input:** head = [3,2,0,-4], pos = 1
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Input:** head = [1,2], pos = 0
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

**Example 3:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

**Input:** head = [1], pos = -1
**Output:** false
**Explanation:** There is no cycle in the linked list.

**Constraints:**

- The number of the nodes in the list is in the range `[0, 104]`.
- `-105 <= Node.val <= 105`
- `pos` is `-1` or a **valid index** in the linked-list.

**Follow up:** Can you solve it using `O(1)` (i.e. constant) memory?

### Problem Analysis:

1. High-level strategy:
    
    - The algorithm uses two pointers, slow and fast, both initially set to the head of the linked list.
    - The fast pointer moves two steps at a time while the slow pointer moves one step at a time.
    - If there's a cycle, eventually the fast pointer will meet the slow pointer (they'll be at the same node).
    - If there's no cycle, the fast pointer will reach the end of the list before the slow pointer.
    - Thus, if the fast pointer ever reaches the end of the list (fast or fast.next becomes None), it means there's no cycle and the function returns False. Otherwise, if the fast and slow pointers meet at some point, it indicates a cycle and the function returns True.
    - this is also called [Floyd’s Cycle Finding Algorithm](https://www.geeksforgeeks.org/floyds-cycle-finding-algorithm/)
1. Complexity:
    
    - Let n be the number of nodes in the linked list.
    - Both slow and fast pointers traverse at most n nodes.
    - Hence, the time complexity of this solution is O(n).
    - The space complexity is O(1) since only a constant amount of extra space is used for the pointers.

## Solutions:

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = fast = head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

## Similar Questions