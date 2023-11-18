---
last_reviewed: 2023-11-18
title: 1838 Frequency of the Most Frequent Element - Medium
excerpt: "-"
tags:
  - solution
  - binary-search
  - sliding-window
---
## Problem:
The **frequency** of an element is the number of times it occurs in an array.

You are given an integer array `nums` and an integer `k`. In one operation, you can choose an index of `nums` and increment the element at that index by `1`.

Return _the **maximum possible frequency** of an element after performing **at most**_ `k` _operations_.

**Example 1:**

**Input:** nums = [1,2,4], k = 5
**Output:** 3
**Explanation:** Increment the first element three times and the second element two times to make nums = [4,4,4].
4 has a frequency of 3.

**Example 2:**

**Input:** nums = [1,4,8,13], k = 5
**Output:** 2
**Explanation:** There are multiple optimal solutions:
- Increment the first element three times to make nums = [4,4,8,13]. 4 has a frequency of 2.
- Increment the second element four times to make nums = [1,8,8,13]. 8 has a frequency of 2.
- Increment the third element five times to make nums = [1,4,13,13]. 13 has a frequency of 2.

**Example 3:**

**Input:** nums = [3,9,6], k = 2
**Output:** 1

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`
- `1 <= k <= 105`

### Problem Analysis:

- **Sorting:**
    - The solution starts by sorting the input array `nums`. Sorting is a crucial step to maximize the frequency of the most frequent element. It helps in bringing similar elements close to each other, allowing for efficient frequency calculations.

- **Sliding Window:**
    - A sliding window approach is employed using two pointers, `left` and `right`, to iterate through the sorted array.
    - The `current_sum` variable keeps track of the sum of elements within the current window.
    
-  **Frequency Calculation:**
    - The algorithm calculates the frequency of elements within the current window.
    - If the number of operations required to make all elements in the window equal is greater than `k`, the window is shrunk by incrementing `left`.

- **Updating Maximum Frequency:**
    - The maximum frequency encountered so far is updated during each iteration.
    
- **Result:**
    - The final result is the maximum frequency of any element after performing at most `k` operations.


- **Time Complexity: O(n log n)**  
    - The most significant factor contributing to the time complexity is the sorting step, which has a time complexity of O(n log n) using the built-in `sort` function. The subsequent sliding window traversal takes linear time.
    
- **Space Complexity: O(1)**
    - The space complexity is constant because the algorithm uses only a constant amount of extra space. The variables `left`, `right`, `max_freq`, and `current_sum` occupy constant space, and the sorting is done in-place, so no additional space is used.

## Solutions:

```python
class Solution:
    def maxFrequency(self, nums: List[int], k: int) -> int:
        nums.sort()
        left = 0
        max_freq = 0
        current_sum = 0

        for right in range(len(nums)):
            current_sum += nums[right]

            # Shrink the window if > k operations not possible
            while (right - left + 1) * nums[right] - current_sum > k:
                current_sum -= nums[left]
                left += 1

            max_freq = max(max_freq, right - left + 1)

        return max_freq        
```

## Similar Questions