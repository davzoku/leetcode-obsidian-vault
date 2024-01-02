---
last_reviewed: 2024-01-02
title: 2610 Convert an Array Into a 2D Array With Conditions - Medium
excerpt: "-"
tags:
  - solution
---
## Problem:
You are given an integer array `nums`. You need to create a 2D array from `nums` satisfying the following conditions:

- The 2D array should contain **only** the elements of the array `nums`.
- Each row in the 2D array contains **distinct** integers.
- The number of rows in the 2D array should be **minimal**.

Return _the resulting array_. If there are multiple answers, return any of them.

**Note** that the 2D array can have a different number of elements on each row.

**Example 1:**

**Input:** nums = [1,3,4,1,2,3,1]
**Output:** `[[1,3,4,2],[1,3],[1]]`
**Explanation:** We can create a 2D array that contains the following rows:
- 1,3,4,2
- 1,3
- 1
All elements of nums were used, and each row of the 2D array contains distinct integers, so it is a valid answer.
It can be shown that we cannot have less than 3 rows in a valid array.

**Example 2:**

**Input:** nums = [1,2,3,4]
**Output:** `[[4,3,2,1]]`
**Explanation:** All elements of the array are distinct, so we can keep all of them in the first row of the 2D array.

**Constraints:**

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= nums.length`

### Problem Analysis:

**High-Level Strategy:**
- The goal of this solution seems to be organizing a given list of integers into a matrix based on their occurrences. The matrix is constructed such that each row represents a unique integer, and the elements of the row are the occurrences of that integer in the input list.

**Complexity:**
- Let n be the length of the input list `nums`.
- The solution iterates through each element in `nums` once, and for each element, it performs constant time operations (dictionary lookups, list appends). Therefore, the time complexity is O(n).
- The space complexity is also O(n) since the solution uses a dictionary (`count`) to store the count of occurrences and a list (`res`) to store the resulting matrix.

## Solutions:

```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        count = defaultdict(int)
        res = []
        for n in nums:
            # get current row from count 
            row = count[n]
            # if they matches, we need to add row
            if len(res) == row:
                res.append([])
            
            res[row].append(n)
            count[n] += 1

        return res
```

## Similar Questions