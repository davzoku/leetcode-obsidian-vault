---
last_reviewed: 2024-05-02
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Given an integer array `nums` that **does not contain** any zeros, find **the largest positive** integer `k` such that `-k` also exists in the array.

Return _the positive integer_ `k`. If there is no such integer, return `-1`.

**Example 1:**

**Input:** nums = [-1,2,-3,3]
**Output:** 3
**Explanation:** 3 is the only valid k we can find in the array.

**Example 2:**

**Input:** nums = [-1,10,6,7,-7,1]
**Output:** 7
**Explanation:** Both 1 and 7 have their corresponding negative values in the array. 7 has a larger value.

**Example 3:**

**Input:** nums = [-10,8,6,7,-2,-3]
**Output:** -1
**Explanation:** There is no a single valid k, we return -1.

**Constraints:**

- `1 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`
- `nums[i] != 0`

### Problem Analysis:
1. **High-level strategy:**
   - The high-level strategy of this solution is to efficiently find the largest positive integer `k` such that `-k` also exists in the given array `nums`.
   - The solution utilizes the fact that the input array is sorted. Sorting the array allows us to use a two-pointer approach, which enables us to efficiently search for pairs that sum up to zero.
   - We initialize two pointers, `left` and `right`, pointing to the start and end of the sorted array, respectively.
   - We iterate through the array using these pointers, comparing the sum of the elements at `left` and `right` indices with zero.
   - If the sum is zero, it means we found a pair of numbers whose sum is zero. We update `max_k` to be the maximum of its current value and the absolute value of the number at `left` index.
   - We continue this process until `left` is less than `right`, ensuring that we cover all possible pairs in the array.

2. **Complexity:**
   - Sorting the array takes O(n log n) time complexity, where n is the number of elements in the array.
   - The two-pointer approach inside the loop runs in O(n) time complexity since each pointer moves at most n times (where n is the size of the array) until they meet or cross each other.
   - Therefore, the overall time complexity of the solution is O(n log n) due to the sorting step.
   - The space complexity is O(1) since the solution only uses a constant amount of extra space regardless of the size of the input array.
## Solutions:

```python
class Solution:
    def findMaxK(self, nums: List[int]) -> int:
        nums.sort()
        max_k = -1
        left, right = 0, len(nums) - 1
        
        while left < right:
            if nums[left] + nums[right] == 0:
                max_k = max(max_k, abs(nums[left]))
                left += 1
                right -= 1
                break
            elif nums[left] + nums[right] < 0:
                left += 1
            else:
                right -= 1
        
        return max_k
```

## Similar Questions