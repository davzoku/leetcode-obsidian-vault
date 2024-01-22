---
last_reviewed: 2024-01-22
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
You have a set of integers `s`, which originally contains all the numbers from `1` to `n`. Unfortunately, due to some error, one of the numbers in `s` got duplicated to another number in the set, which results in **repetition of one** number and **loss of another** number.

You are given an integer array `nums` representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return _them in the form of an array_.

**Example 1:**

**Input:** nums = [1,2,2,4]
**Output:** [2,3]

**Example 2:**

**Input:** nums = [1,1]
**Output:** [1,2]

**Constraints:**

- `2 <= nums.length <= 104`
- `1 <= nums[i] <= 104`

### Problem Analysis:
### Solution 1
1. **High-Level Strategy:**
    - The code uses a Counter to count the occurrences of each element in the given list `nums`.
    - It then identifies the duplicate by finding the element with the maximum count using the `max` function and the `key` parameter.
    - The missing element is determined by iterating over the range from 1 to the length of `nums` + 1 and finding the first element not present in the Counter.
2. **Complexity Analysis:**
    - The time complexity of the solution is dominated by the loop that iterates over the range from 1 to the length of `nums` + 1. In the worst case, this loop runs in O(n) time, where n is the length of the input list.
    - The Counter construction takes O(n) time, and finding the maximum count takes O(1) time.
    - The overall time complexity is O(n).
    - The space complexity is O(n) due to the Counter, which stores the count of each unique element in the input list.

### Solution 2

1. **High-Level Strategy:**
    
    - This solution takes advantage of the properties of the sum of natural numbers from 1 to n.
    - It calculates the expected sum using the formula `n * (n + 1) // 2`, which is the sum of all unique elements if there were no duplicates or missing elements.
    - It then calculates the actual sum of the given list `nums`.
    - The difference between the actual sum and the sum of unique elements gives the duplicate, and the difference between the expected sum and the actual sum gives the missing element.
    - The solution directly computes the duplicate and missing elements without explicitly counting occurrences using loops or data structures.
2. **Complexity Analysis:**
    
    - Calculating the expected sum takes constant time, O(1).
    - Computing the actual sum of `nums` takes O(n) time, where n is the length of the input list.
    - Constructing a set from `nums` takes O(n) time as well.
    - The overall time complexity is dominated by the summation and set operations, resulting in O(n) time complexity.
    - The space complexity is O(n) due to the space required for the set, which stores the unique elements of the input list.
## Solutions:

### Solution 1:

```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        count = Counter(nums)
        duplicate = max(count, key=count.get)
        missing = 0
        for i in range(1, len(nums)+1):
            if i not in count.keys():
                missing = i
        return [duplicate, missing]
```

### Solution 2:
```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        n = len(nums)
        expected_sum = n * (n + 1) // 2  # Sum of natural numbers from 1 to n

        actual_sum = sum(nums)
        duplicate = actual_sum - sum(set(nums))  # Duplicate is the difference between actual sum and sum of unique elements

        missing = expected_sum - (actual_sum - duplicate)  # Missing is the difference between expected sum and actual sum

        return [duplicate, missing]
```
## Similar Questions