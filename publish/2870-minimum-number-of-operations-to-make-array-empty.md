---
last_reviewed: 2024-01-04
title: 2870 Minimum Number of Operations to Make Array Empty - Medium
excerpt: "-"
tags:
  - solution
  - greedy
  - math
  - counting
  - arrays
---
## Problem:
You are given a **0-indexed** array `nums` consisting of positive integers.

There are two types of operations that you can apply on the array **any** number of times:

- Choose **two** elements with **equal** values and **delete** them from the array.
- Choose **three** elements with **equal** values and **delete** them from the array.

Return _the **minimum** number of operations required to make the array empty, or_ `-1` _if it is not possible_.

**Example 1:**

**Input:** nums = [2,3,3,2,2,4,2,3,4]
**Output:** 4
**Explanation:** We can apply the following operations to make the array empty:
- Apply the first operation on the elements at indices 0 and 3. The resulting array is nums = [3,3,2,4,2,3,4].
- Apply the first operation on the elements at indices 2 and 4. The resulting array is nums = [3,3,4,3,4].
- Apply the second operation on the elements at indices 0, 1, and 3. The resulting array is nums = [4,4].
- Apply the first operation on the elements at indices 0 and 1. The resulting array is nums = [].
It can be shown that we cannot make the array empty in less than 4 operations.

**Example 2:**

**Input:** nums = [2,1,2,2,3,3]
**Output:** -1
**Explanation:** It is impossible to empty the array.

**Constraints:**

- `2 <= nums.length <= 105`
- `1 <= nums[i] <= 106`

### Problem Analysis:
**High Level Strategy:**
- As long as no element appears only once, there is always a possible solution. 
- Simply consider the case of `i%3`
	- if the remainder is 2, it is straightforward, we can just add 1 more operations to account for the pair
	- if the remainder is 1, eg. 10%3 = 1,
		- 10 can be 5 pairs -> 5
		- 3 triplets and 1 standalone (not possible) 
		- or it can be 2 triplets and 2 pairs -> 4. This is also equal to 10%3 + 1
	- Hence both conditions can be simplified to + 1.

**Complexity:**

- **Time Complexity:** The solution iterates through the counts of each number in the `count_dict`, which takes O(N) time, where N is the length of the input array.
- **Space Complexity:** Additional space is used for the `count_dict`, which takes O(N) space, where N is the length of the input array.

## Solutions:

```python
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        count_dict = Counter(nums)
        res = 0
        
        for i in count_dict.values():
            if i == 1:
                return -1 
            res += i//3
            if i % 3:
                res += 1
        return res
```

## Similar Questions