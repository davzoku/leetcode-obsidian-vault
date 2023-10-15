---
last_reviewed: 2023-10-15
title: 1646 Get Maximum in Generated Array - Easy
excerpt: "-"
tags:
  - solution
  - arrays
---
## Problem:

You are given an integer `n`. A **0-indexed** integer array `nums` of length `n + 1` is generated in the following way:

- `nums[0] = 0`
- `nums[1] = 1`
- `nums[2 * i] = nums[i]` when `2 <= 2 * i <= n`
- `nums[2 * i + 1] = nums[i] + nums[i + 1]` when `2 <= 2 * i + 1 <= n`

Return _the **maximum** integer in the array_ `nums`​​​.

**Example 1:**

**Input:** n = 7
**Output:** 3
**Explanation:** According to the given rules:
  nums[0] = 0
  nums[1] = 1
  nums[(1 * 2) = 2] = nums[1] = 1
  nums[(1 * 2) + 1 = 3] = nums[1] + nums[2] = 1 + 1 = 2
  nums[(2 * 2) = 4] = nums[2] = 1
  nums[(2 * 2) + 1 = 5] = nums[2] + nums[3] = 1 + 2 = 3
  nums[(3 * 2) = 6] = nums[3] = 2
  nums[(3 * 2) + 1 = 7] = nums[3] + nums[4] = 2 + 1 = 3
Hence, nums = [0,1,1,2,1,3,2,3], and the maximum is max(0,1,1,2,1,3,2,3) = 3.

**Example 2:**

**Input:** n = 2
**Output:** 1
**Explanation:** According to the given rules, nums = [0,1,1]. The maximum is max(0,1,1) = 1.

**Example 3:**

**Input:** n = 3
**Output:** 2
**Explanation:** According to the given rules, nums = [0,1,1,2]. The maximum is max(0,1,1,2) = 2.

**Constraints:**

- `0 <= n <= 100`

### Problem Analysis:

## Solutions:

Straightforward solution based on requirements

```python
class Solution(object):
    def getMaximumGenerated(self, n):
        """
        :type n: int
        :rtype: int
        """
        tmp = []

        for i in range(n+1):
            if i == 0:
                tmp.append(0)
            elif i == 1:
                tmp.append(1)
            elif i%2 == 0:
                tmp.append(tmp[i//2])
            else: 
                tmp.append(tmp[i//2] + tmp[i//2+1])


        return max(tmp)
```
![[1646-1.png]]

```python
class Solution(object):
    def getMaximumGenerated(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0 or n == 1: 
            return n

        max_val = 0
        #initialize array
        tmp = [0] * (n + 1)

        tmp[1] = 1            
        for i in range(2,n+1):  
            if i%2 == 0:
                tmp[i] = (tmp[i//2])
            else: 
                tmp[i]= (tmp[i//2] + tmp[i//2+1])
            max_val = max(max_val, tmp[i])
        return max_val
```
![[1646-2.png]]
## Similar Questions