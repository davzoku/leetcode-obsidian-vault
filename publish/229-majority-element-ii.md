---
last_reviewed: 2023-10-08
title: 229 Majority Element II - Medium
excerpt: "-"
tags:
  - arrays
  - solution
---
## Problem:

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** [3]

**Example 2:**

**Input:** nums = [1]
**Output:** [1]

**Example 3:**

**Input:** nums = [1,2]
**Output:** [1,2]

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-109 <= nums[i] <= 109`

**Follow up:** Could you solve the problem in linear time and in `O(1)` space?
### Problem Analysis:

- Very easy to come up with Time O(n) and Space O(n) solutions with Dictionary.
- Iterate through the list and construct a dictionary to get the count for each integer and return a list with integer with count more than n/3
- **Note:** logically, this array should be at most of length 2.

## Solutions:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        if len(nums) == 1:
            return nums        
        min_count = len(nums) // 3
        count = {}
        output = set()
        for n in nums:
            count[n] = count.get(n, 0) + 1
            if count[n] > min_count:
                output.add(n)

        return output
```
## Alternative Solution

- Boyer-Moore Majority Voting Algorithm

## Similar Questions