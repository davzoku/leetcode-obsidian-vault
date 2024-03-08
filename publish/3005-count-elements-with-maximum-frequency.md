---
last_reviewed: 2024-03-08
title: 3005 Count Elements with Maximum Frequency - Easy
excerpt: "-"
tags:
  - solution
  - counting
  - hashmap
---
## Problem:
You are given an array `nums` consisting of **positive** integers.

Return _the **total frequencies** of elements in_ `nums` _such that those elements all have the **maximum** frequency_.

The **frequency** of an element is the number of occurrences of that element in the array.

**Example 1:**

**Input:** nums = [1,2,2,3,1,4]
**Output:** 4
**Explanation:** The elements 1 and 2 have a frequency of 2 which is the maximum frequency in the array.
So the number of elements in the array with maximum frequency is 4.

**Example 2:**

**Input:** nums = [1,2,3,4,5]
**Output:** 5
**Explanation:** All elements of the array have a frequency of 1 which is the maximum.
So the number of elements in the array with maximum frequency is 5.

**Constraints:**

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`

### Problem Analysis:
1. **High-level Strategy:**
    
    - The solution first creates a counter `count` to count the occurrences of each element in the input list `nums`.
    - It then finds the maximum frequency (`max_freq`) among the counts of elements in the counter.
    - After that, it iterates through the values of the counter, and if any value matches the maximum frequency, it adds that frequency to the `output`.
    - Finally, it returns the sum of frequencies of elements having the maximum frequency.
2. **Complexity:**
    
    - Let n be the length of the input list `nums`.
    - Creating the counter takes O(n) time as it iterates through the list once.
    - Finding the maximum frequency takes O(n) time as well since it iterates through all values in the counter.
    - The loop to iterate through the values of the counter takes O(n) time.
    - Overall, the time complexity of the solution is O(n).
    - The space complexity is also O(n) because the counter dictionary holds at most n unique elements from the input list.

## Solutions:

```python
class Solution:
    def maxFrequencyElements(self, nums: List[int]) -> int:
        count = Counter(nums)
        max_freq = max(count.values())
        output = 0
        for i in count.values():
            if i == max_freq:
                output += i
        return output
```

## Similar Questions