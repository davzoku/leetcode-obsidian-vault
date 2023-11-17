---
last_reviewed: 2023-11-17
title: 1877 Minimize Maximum Pair Sum in Array - Medium
excerpt: "-"
tags:
  - solution
  - string
  - sorting
---
## Problem:
The pair sum of a pair (a,b) is equal to a + b. The maximum pair sum is the largest pair sum in a list of pairs.

For example, if we have pairs (1,5), (2,3), and (4,4), the maximum pair sum would be max(1+5, 2+3, 4+4) = max(6, 5, 8) = 8.
Given an array nums of even length n, pair up the elements of nums into n / 2 pairs such that:

Each element of nums is in exactly one pair, and
The maximum pair sum is minimized.
Return the minimized maximum pair sum after optimally pairing up the elements.

 

Example 1:

Input: nums = [3,5,2,3]
Output: 7
Explanation: The elements can be paired up into pairs (3,3) and (5,2).
The maximum pair sum is max(3+3, 5+2) = max(6, 7) = 7.
Example 2:

Input: nums = [3,5,4,2,4,6]
Output: 8
Explanation: The elements can be paired up into pairs (3,5), (4,4), and (6,2).
The maximum pair sum is max(3+5, 4+4, 6+2) = max(8, 8, 8) = 8.
 

Constraints:

n == nums.length
2 <= n <= 105
n is even.
1 <= nums[i] <= 105

### Problem Analysis:
- **Sorting:**
  - The function first sorts the given array `nums` in ascending order. Sorting is a crucial step in this solution as it helps in pairing the smallest and largest elements together.

- **Pairing:**
  - The function then iterates through the first half of the sorted array.
  - For each iteration, it calculates the sum of the current element at index `i` and its counterpart at the end of the array (`n - 1 - i`).
  - The result is updated to be the maximum of the current result and the calculated sum.

- **Result:**
  - The final result is the maximum pair sum achieved by pairing the smallest and largest elements.

- **Time Complexity:**
  - O(n log n) due to the sorting operation.
    - The dominant factor is the sorting of the array, which takes O(n log n) time for an array of length n.
    - The subsequent iteration through half of the array takes O(n / 2), which simplifies to O(n) in big-O notation.

- **Space Complexity:**
  - O(1) (constant space).
    - The space used is minimal, as the function only uses a constant amount of extra space regardless of the input size.
    - The sorting operation is typically in-place and does not require additional space proportional to the input size.

## Solutions:

```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        nums.sort()
        n = len(nums)
        result = 0
        
        for i in range(n // 2):
            result = max(result, nums[i] + nums[n - 1 - i])
        
        return result

```

## Similar Questions