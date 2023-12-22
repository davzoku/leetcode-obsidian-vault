---
last_reviewed: 2023-12-22
title: 41 First Missing Positive - Hard
excerpt: "-"
tags:
  - solution
  - arrays
  - sorting
---
## Problem:
Given an unsorted integer array `nums`, return the smallest missing positive integer.

**You must implement an algorithm that runs in `O(n)` time and uses `O(1)` auxiliary space.**

**Example 1:**

**Input:** nums = [1,2,0]
**Output:** 3
**Explanation:** The numbers in the range [1,2] are all in the array.

**Example 2:**

**Input:** nums = [3,4,-1,1]
**Output:** 2
**Explanation:** 1 is in the array but 2 is missing.

**Example 3:**

**Input:** nums = [7,8,9,11,12]
**Output:** 1
**Explanation:** The smallest positive integer 1 is missing.

**Constraints:**

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`

### Problem Analysis:
####   Solution 1:

##### High-Level Strategy:

- Sorts the input list `nums` in ascending order.
- Iterates through the sorted list and finds the first missing positive integer by comparing each element with the current expected positive integer (`res`).
- Increments `res` until a missing positive integer is found.

##### Complexity:

- **Time Complexity:** O(N log N), where N is the length of the input list `nums` due to sorting.
- **Space Complexity:** O(1), as no extra space is used except for variables.

#### Solution 2:

##### High-Level Strategy:

- Utilizes the array itself to represent the solution space `[1, 2, ..., len(nums)+1]`.
- Iterates through the array, placing each element in its correct position if it falls within the range `[1, len(nums)]`.
- Finds the first position where the number is not equal to its index + 1, which represents the first missing positive integer.

##### Complexity:

- **Time Complexity:** O(N), where N is the length of the input list `nums`. Each element is processed at most twice.
- **Space Complexity:** O(1), as no extra space is used except for variables.

#### Comparison:

- Both solutions aim to find the first missing positive integer.
- Solution 2 has a better time complexity since it avoids the sorting step and **meets the requirements of the question**

## Solutions:
### Solution 1 (Sorting)

```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums.sort()
        res = 1
        for num in nums:
            if num == res:
                res += 1

        return res
```

### Solution 2 (Ideal)

```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        # solution space: [1, ..., len(nums)+1]
        # [0, 1, 2] indexes
        # [1, 2, 3] ideal values should be i+1 of its index
        n = len(nums)

        for i in range(n):
            # while value num[i] is within ideal values, swap it to its ideal position
            while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
                nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]

        # find the first position where the number is not equal to its index + 1
        for i in range(n):
            if nums[i] != i + 1:
                return i + 1

        # otherwise return the next positive integer
        return n + 1
```
## Similar Questions
- [[268-missing-number]]