---
last_reviewed: 2023-11-21
title: 1814 Count Nice Pairs in an Array - Medium
excerpt: "-"
tags:
  - solution
  - hashmap
---
## Problem:
You are given an array `nums` that consists of non-negative integers. Let us define `rev(x)` as the reverse of the non-negative integer `x`. For example, `rev(123) = 321`, and `rev(120) = 21`. A pair of indices `(i, j)` is **nice** if it satisfies all of the following conditions:

- `0 <= i < j < nums.length`
- `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])`

Return _the number of nice pairs of indices_. Since that number can be too large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** nums = [42,11,1,97]
**Output:** 2
**Explanation:** The two pairs are:
 - (0,3) : 42 + rev(97) = 42 + 79 = 121, 97 + rev(42) = 97 + 24 = 121.
 - (1,2) : 11 + rev(1) = 11 + 1 = 12, 1 + rev(11) = 1 + 11 = 12.

**Example 2:**

**Input:** nums = [13,10,35,24,76]
**Output:** 4

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`

### Problem Analysis:

- For each number, it calculates the difference between the number and its reversed counterpart.
- uses a dictionary `freq` to keep track of the frequencies of these differences.
- avoid counting first occurence in the pair

- **Time Complexity:**
    - O(N * K) where N is the number of elements in `nums` and K is the average number of digits in each element.
        - The solution iterates through each number in `nums`, and for each number, it performs the conversion to a reversed string (O(K) operations).
        
- **Space Complexity:**
    - O(N) for the `freq` dictionary.
        - The space complexity is dominated by the dictionary, which keeps track of the frequencies of differences between numbers and their reversed counterparts. The additional variables (`MOD`, `res`, `num`, `diff`) use constant space.

## Solutions:

```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        MOD = 10**9 + 7
        freq = {}
        res = 0

        for num in nums:
            # calculate diff between num and its reverse
            diff = num - int(str(num)[::-1])
            freq[diff] = freq.get(diff, 0) + 1
            # dont count first occurence
            res += freq[diff] - 1
            
        return res % MOD
```

## Similar Questions