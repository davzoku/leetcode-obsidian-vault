---
last_reviewed: 2023-10-09
title: 213 House Robber II - Medium
excerpt: "-"
tags:
  - "#dynamic-programming"
---
## Problem:
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Example 1:**

**Input:** nums = [2,3,2]
**Output:** 3
**Explanation:** You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

**Example 2:**

**Input:** nums = [1,2,3,1]
**Output:** 4
**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

**Example 3:**

**Input:** nums = [1,2,3]
**Output:** 3

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

### Problem Analysis:

- similar to [[198-house-robber]], with 1 additional constraint that the **list of houses are arranged in a circle**
- base case is when the length is 1
- then we have to perform dp on 2 subarrays. _1 without the first element_ and _1 without the last element_.
- then we just have to return the max of these 3 values

## Solutions:

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # base case: length 1, return the first element
        # then do dp on 2 subarray; 1 without the first element, 1 without the last element
        return max(nums[0], self.dynamic_programming(nums[1:]), self.dynamic_programming(nums[:-1]))

    def dynamic_programming(self, nums: List[int]) -> int:
        rob1, rob2 = 0, 0
        
        for n in nums:
            temp = max(rob1 + n, rob2)
            rob1 = rob2
            rob2 = temp
        return rob2
```

## Similar Questions

- [[198-house-robber]]
- [[337-house-robber-iii]]
- [[2560-house-robber-iv]]