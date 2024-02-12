---
last_reviewed: 2024-02-12
title: 169 Majority Element - Easy
excerpt: "-"
tags:
  - solution
  - hashmap
  - boyer-moore-majority-vote
---
## Problem:
Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

**Constraints:**

- `n == nums.length`
- `1 <= n <= 5 * 104`
- `-109 <= nums[i] <= 109`

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

### Problem Analysis:
1. **High-Level Strategy**:
- The solution uses the Boyer-Moore Majority Vote Algorithm, which is a clever approach to find the majority element in a sequence without using extra memory.
- The algorithm starts with a `count` initialized to 0 and a `candidate` initialized to None.
- It iterates through the elements of the array:
	- If `count` becomes 0, it updates the `candidate` to the current element because it means all occurrences of the previous `candidate` have been canceled out by occurrences of other elements so far.
	- If the current element matches the `candidate`, `count` is incremented by 1; otherwise, `count` is decremented by 1.
- At the end of the iteration, `candidate` will hold the majority element.

1. **Complexity Analysis**:
- Time Complexity: The algorithm iterates through the array once, so the time complexity is O(n), where n is the number of elements in the input list `nums`.
- Space Complexity: The algorithm uses only constant extra space, regardless of the size of the input array. Therefore, the space complexity is O(1).

## Solutions:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = 0
        candidate = None
        
        for num in nums:
            if count == 0:
                candidate = num
            count += (1 if num == candidate else -1)
        
        return candidate
```

## Similar Questions
- [[229-majority-element-ii]]