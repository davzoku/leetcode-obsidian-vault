---
last_reviewed: 2024-01-05
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Given an integer array `nums`, return _the length of the longest **strictly increasing**__**subsequence**_.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]
**Output:** 4
**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]
**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]
**Output:** 1

**Constraints:**

- `1 <= nums.length <= 2500`
- `-104 <= nums[i] <= 104`

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

### Problem Analysis:
**High Level Strategy:**
- The `dp` array is used to store the length of the longest increasing subsequence ending at each index.
- We iterate through the array, and for each element, we compare it with previous elements to determine the length of the longest increasing subsequence ending at the current index.
- The final result is the maximum value in the `dp` array, representing the overall longest increasing subsequence.

**Complexity:**
- Time Complexity: O(N^2) - There are nested loops for each element, and in the worst case, we compare each element with all previous elements.
- Space Complexity: O(N) - We use an additional array (`dp`) of the same length as the input array to store intermediate results.

## Solutions:

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)

        for i in range(len(nums)):
            for j in range(i):
                # If the current element is greater than the previous element,
                # update the length of the longest increasing subsequence at the current index
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)

        return max(dp)

```

## Similar Questions