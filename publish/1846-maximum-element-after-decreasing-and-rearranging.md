---
last_reviewed: 2023-11-15
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
You are given an array of positive integers `arr`. Perform some operations (possibly none) on `arr` so that it satisfies these conditions:

- The value of the **first** element in `arr` must be `1`.
- The absolute difference between any 2 adjacent elements must be **less than or equal to** `1`. In other words, `abs(arr[i] - arr[i - 1]) <= 1` for each `i` where `1 <= i < arr.length` (**0-indexed**). `abs(x)` is the absolute value of `x`.

There are 2 types of operations that you can perform any number of times:

- **Decrease** the value of any element of `arr` to a **smaller positive integer**.
- **Rearrange** the elements of `arr` to be in any order.

Return _the **maximum** possible value of an element in_ `arr` _after performing the operations to satisfy the conditions_.

**Example 1:**

**Input:** arr = [2,2,1,2,1]
**Output:** 2
**Explanation:** 
We can satisfy the conditions by rearranging `arr` so it becomes `[1,2,2,2,1]`.
The largest element in `arr` is 2.

**Example 2:**

**Input:** arr = [100,1,1000]
**Output:** 3
**Explanation:** 
One possible way to satisfy the conditions is by doing the following:
1. Rearrange `arr` so it becomes `[1,100,1000]`.
2. Decrease the value of the second element to 2.
3. Decrease the value of the third element to 3.
Now `arr = [1,2,3], which` satisfies the conditions.
The largest element in `arr is 3.`

**Example 3:**

**Input:** arr = [1,2,3,4,5]
**Output:** 5
**Explanation:** The array already satisfies the conditions, and the largest element is 5.

**Constraints:**

- `1 <= arr.length <= 105`
- `1 <= arr[i] <= 109`

### Problem Analysis:
- **Initialization:**
    - Store the length of the array in a variable (`n`).
    - Initialize a variable (`max_val`) to track the maximum valid value.
- **Single Pass Update:**
    - Iterate through the array once.
    - Update each element in the array to be the minimum of its current value and the previous element plus one.
- **Maximum Value Tracking:**
    - During the iteration, track the maximum valid value encountered in the `max_val` variable.
- **Result:**
    - Return the maximum valid value (`max_val`) as the result.

- **Time Complexity:**
    - O(N * log(N)) due to the sort operation.
        - Sorting the array has a time complexity of O(N * log(N)), where N is the length of the array.
    - The subsequent single pass through the array has a linear time complexity of O(N).
    - Overall, the dominant factor is the sort operation.
- **Space Complexity:**
    - O(1) (constant space).
        - The algorithm uses a constant amount of extra space, regardless of the input size.
        - Sorting is typically in-place and doesn't require additional space proportional to the input size.

## Solutions:

```python
class Solution:
    def maximumElementAfterDecrementingAndRearranging(self, arr: List[int]) -> int:
        n = len(arr)
        arr.sort()

        max_val = 1
        for i in range(1, n):
            max_val = min(arr[i], max_val + 1)

        return max_val
```

## Similar Questions