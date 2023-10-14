---
last_reviewed: 2023-10-13
title: 53 Maximum Subarray - Medium
excerpt: "-"
tags:
  - greedy
  - solution
---
## Problem:

Given an integer array `nums`, find the 

subarray

 with the largest sum, and return _its sum_.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1
**Explanation:** The subarray [1] has the largest sum 1.

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

### Problem Analysis:

- use greedy approach; specifically Kadene's Algorithm

## Solutions:

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # max_so_far: overall maximum sum found in the array up to the current position in the iteration.
        # max_ending_here: maximum sum of subarrays that include the current element
        max_so_far = max_ending_here = nums[0]

        for num in nums[1:]:
            max_ending_here = max(num, max_ending_here + num)
            max_so_far = max(max_so_far, max_ending_here)

        return max_so_far        
```

## Similar Questions