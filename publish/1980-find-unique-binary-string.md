---
last_reviewed: 2023-11-16
title: 1980 Find Unique Binary String - Medium
excerpt: "-"
tags:
  - solution
  - backtracking
  - string
  - cantors-diagonalization
---
## Problem:
Given an array of strings `nums` containing `n` **unique** binary strings each of length `n`, return _a binary string of length_ `n` _that **does not appear** in_ `nums`_. If there are multiple answers, you may return **any** of them_.

**Example 1:**

**Input:** nums = ["01","10"]
**Output:** "11"
**Explanation:** "11" does not appear in nums. "00" would also be correct.

**Example 2:**

**Input:** nums = ["00","01"]
**Output:** "11"
**Explanation:** "11" does not appear in nums. "10" would also be correct.

**Example 3:**

**Input:** nums = ["111","011","001"]
**Output:** "101"
**Explanation:** "101" does not appear in nums. "000", "010", "100", and "110" would also be correct.

**Constraints:**

- `n == nums.length`
- `1 <= n <= 16`
- `nums[i].length == n`
- `nums[i]` is either `'0'` or `'1'`.
- All the strings of `nums` are **unique**.

### Problem Analysis:

**Credits to [sl33](https://leetcode.com/problems/find-unique-binary-string/solutions/3935401/o-n-time-o-n-space-solution-explained/)

We are given some binary strings from 0 to n, all of equal length. we need to return any one of the missing numbers.

- Approach 1: Backtracking  
    use backtracking to explore all possible strings of the same length as the input string length and check if it is the missing string i.e. it is not in the input list. Convert the input list of strings to hash set to search in O(1) time.
- Approach 2  
    traverse all decimal numbers in the range 0 to n. Find the binary and check if it is present in the input list. You can also first convert all numbers to binary strings and then check, but you would be doing some unnecessary conversions. Convert the input to hash set to search in O(1) time.
- **Approach 3: Cantor's Diagonalization**
    According to this, a binary number missing from a binary sequence can be constructed by flipping the 1st bit of s1, the 2nd bit of s2, ... and the nth bit of sn.  
    For example:  
    input strings = ['111', '001', '010'] i.e [7, 1, 0]  
    missing numbers are 3, 4, 5  
    we need only one missing number and the first missing number can be formed as:  
    flip 1st bit of num1 + flip 2nd bit of num2 + flip 3rd bit of num3  
    0 + 1 + 1 = 011 = 3 (+ represent concatenation here)

# Approach

# Complexity

- Time complexity:
    - Approach 1  
        O(recursion breadth) → O(calls at each level ^ total levels) → O(2n^nn)
    - Approach 2  
        O(set + traversal * decimal to binary conversion) → O(n + n * log(number)) → O(n + n) → O(n)
    - Approach 3  
        O(list comprehension + join) → O(n + size of a binary string) → O(n + size of binary of 16 because n <= 16) → O(n + 5) → O(n)

- Space complexity:
    - Approach 1  
        O(recursion stack) → O(recursion depth/levels) → O(n)
    - Approach 2  
        O(set + decimal to binary conversion) → O(n + log(number)) → O(n)
    - Approach 3  
        O(list comprehension) → O(n)
## Solutions:

```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        
        # appraoch 1

        nums = set(nums)

        def backtrack(i: int, path: List[str]) -> str:
            if i == len(nums):
                res = ''.join(path)
                return res if res not in nums else None
            res = backtrack(i + 1, path)
            if res: 
                return res
            path[i] = '1'
            res = backtrack(i + 1, path)
            if res: 
                return res
            
        return backtrack(0, ['0' for s in nums])
        

        # appraoch 2

        nums_set = set(nums)
        n = len(nums)
        for num in range(n + 1):
            cur = f'{num:0>{n}b}'
            if cur not in nums:
                return cur

        # approach 3

        res = ['1' if num[i] == '0' else '0' for i, num in enumerate(nums)]
        return ''.join(res)
```

## Similar Questions