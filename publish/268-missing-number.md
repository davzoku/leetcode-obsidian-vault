---
last_reviewed: 2023-12-22
title: 268 Missing Number - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - sorting
---
## Problem:
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return _the only number in the range that is missing from the array._

**Example 1:**

**Input:** nums = [3,0,1]
**Output:** 2
**Explanation:** n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.

**Example 2:**

**Input:** nums = [0,1]
**Output:** 2
**Explanation:** n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.

**Example 3:**

**Input:** nums = [9,6,4,2,3,5,7,0,1]
**Output:** 8
**Explanation:** n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.

**Constraints:**

- `n == nums.length`
- `1 <= n <= 104`
- `0 <= nums[i] <= n`
- All the numbers of `nums` are **unique**.

**Follow up:** Could you implement a solution using only `O(1)` extra space complexity and `O(n)` runtime complexity?

### Problem Analysis:
This question is very similar to [[41-find-missing-positive]]. The 2 solutions from problem 41 will work with minor modifications. Additionally, given the additional constraint that **array `nums` containing `n` distinct numbers in the range `[0, n]`**, we can use the sum of arithmetic series to solve this question.

##### High-Level Strategy:

- Sorts the input list `nums` in ascending order.
- Iterates through the sorted list and finds the first missing positive integer by comparing each element with the current expected positive integer (`res`).
- Increments `res` until a missing positive integer is found.

##### Complexity:

- **Time Complexity:** O(N log N), where N is the length of the input list `nums` due to sorting.
- **Space Complexity:** O(1), as no extra space is used except for variables.

#### Solution 2:

##### High-Level Strategy:

- Utilizes the array itself to represent the solution space `[0, 1, ..., len(nums)]`.
- Iterates through the array, placing each element in its correct position if it falls within the range `[0, len(nums)-1]`.
- Finds the first position where the number is not equal to its index + 1, which represents the first missing positive integer.

##### Complexity:

- **Time Complexity:** O(N), where N is the length of the input list `nums`. Each element is processed at most twice.
- **Space Complexity:** O(1), as no extra space is used except for variables.

#### Comparison:

- Both solutions aim to find the first missing positive integer.
- Solution 2 has a better time complexity since it avoids the sorting step and **meets the requirements of the question**

#### Solution 3:

##### High-Level Strategy:

- This code works by calculating the sum of the expected sequence of numbers from 0 to n using the formula for the sum of an arithmetic series (`n * (n + 1) / 2`). It then subtracts the sum of the actual numbers in the input list from this expected sum, and the result is the missing number.

##### Complexity:

1. Calculating the length of the input list takes O(1) time.
2. Calculating the expected sum using the formula takes O(1) time.
3. Computing the sum of the input list using `sum(nums)` takes O(n) time, where n is the length of the input list.
4. The subtraction operation `expect - sum(nums)` takes O(1) time.

Therefore, the overall time complexity is O(n).

1. The only additional space used is for the variable `expect`, which is O(1).

The space complexity is O(1) as well.


## Solutions:

### Solution 1 (Sorting)
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        nums.sort()
        res = 0
        for num in nums:
            if num == res:
                res += 1
        return res        
```

### Solution 2 (Swapping)
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        # solution space: [1, ..., len(nums)+1]
        # [0, 1, 2] indexes
        # [0, 1, 2] ideal values should be i of its index
        n = len(nums)

        for i in range(n):
            # while value num[i] is within ideal values, swap it to its ideal position
            while 0 <= nums[i] < n and nums[nums[i]] != nums[i]:
                nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        
        # find the first position where the number is not equal to its index
        for i in range(n):
            if nums[i] != i:
                return i

        # otherwise return the next positive integer
        return n
```

### Solution 3 (Math)
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        n = len(nums)
        expect = int((n * (n + 1)) / 2) 
        return expect - sum(nums)
```
## Similar Questions
- [[41-find-missing-positive]]