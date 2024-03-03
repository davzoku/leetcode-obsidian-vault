---
last_reviewed: 2024-03-02
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
Given an integer array `nums` sorted in **non-decreasing** order, return _an array of **the squares of each number** sorted in non-decreasing order_.

**Example 1:**

**Input:** nums = [-4,-1,0,3,10]
**Output:** [0,1,9,16,100]
**Explanation:** After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

**Example 2:**

**Input:** nums = [-7,-3,2,3,11]
**Output:** [4,9,9,49,121]

**Constraints:**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` is sorted in **non-decreasing** order.

**Follow up:** Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

### Problem Analysis:
1. **High-Level Strategy:**
    - The solution aims to square each element in the given list `nums` and return a new list containing these squared values in sorted order.
    - It utilizes a generator expression to square each element in `nums` and produces an iterator of squared values.
    - Finally, it applies the `sorted()` function to sort these squared values.
2. **Complexity:**
    - Let's denote `n` as the length of the input list `nums`.
    - Generating squared values for each element in `nums` has a time complexity of O(n) since it iterates through each element once.
    - Sorting the squared values using `sorted()` function has a time complexity of O(n log n), where `n` is the number of squared values.
    - Thus, the overall time complexity of the solution is O(n log n), dominated by the sorting operation.
    - The space complexity of this solution is O(n), as it generates a new list of squared values which could potentially be of the same length as the input list.

## Solutions:

### Solution 1
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted(i*i for i in nums)
```

### Solution 2
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [0] * n
        
        left, right = 0, n - 1
        index = n - 1
        
        while left <= right:
            left_square = nums[left] ** 2
            right_square = nums[right] ** 2
            
            if left_square > right_square:
                result[index] = left_square
                left += 1
            else:
                result[index] = right_square
                right -= 1
                
            index -= 1
        
        return result
```

## Similar Questions