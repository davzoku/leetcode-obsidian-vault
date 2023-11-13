---
last_reviewed: 2023-11-13
title: 946 Validate Stack Sequence - Medium
excerpt: "-"
tags:
  - solution
---
## Problem:

Given two integer arrays `pushed` and `popped` each with distinct values, return `true` _if this could have been the result of a sequence of push and pop operations on an initially empty stack, or_ `false` _otherwise._

**Example 1:**

**Input:** pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
**Output:** true
**Explanation:** We might do the following sequence:
push(1), push(2), push(3), push(4),
pop() -> 4,
push(5),
pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

**Example 2:**

**Input:** pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
**Output:** false
**Explanation:** 1 cannot be popped before 2.

**Constraints:**

- `1 <= pushed.length <= 1000`
- `0 <= pushed[i] <= 1000`
- All the elements of `pushed` are **unique**.
- `popped.length == pushed.length`
- `popped` is a permutation of `pushed`.

### Problem Analysis:
- **Initialization:**
    - Initialize an index `i` and an empty stack.
- **Iteration:**
    - Iterate through the elements in the `pushed` array.
    - For each element, push it onto the stack.
- **Validation:**
    - While the conditions for popping elements from the stack are met (stack is not empty and the top element of the stack equals the current element in `popped`), pop elements from the stack and increment the index `i` in the `popped` array.
- **Result:**
    - After the iteration, check if the stack is empty. If it is, return `True` (the sequences are valid); otherwise, return `False`.

**2. Complexity:**

- **Time Complexity:**
    - O(N), where N is the length of the input arrays (`pushed` and `popped`).
    - Each element is processed once, and each operation inside the loop takes constant time.
- **Space Complexity:**
    - O(N), where N is the length of the input arrays.
    - The space complexity is determined by the stack, and in the worst case, it can grow up to the size of the input arrays.

## Solutions:

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        i = 0
        stack = []
        for n in pushed:
            stack.append(n)
            while i < len(pushed) and stack and popped[i] == stack[-1]:
                stack.pop()
                i += 1

        return not stack
```

## Similar Questions