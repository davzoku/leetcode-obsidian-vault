---
last_reviewed: 2024-05-27
title: 1608 Special Array with X Elements Greater Than Or Equal X - Easy
excerpt: "-"
tags:
  - solution
  - binary-search
  - bisect
  - sorting
  - arrays
---
## Problem:
You are given an array `nums` of non-negative integers. `nums` is considered **special** if there exists a number `x` such that there are **exactly** `x` numbers in `nums` that are **greater than or equal to** `x`.

Notice that `x` **does not** have to be an element in `nums`.

Return `x` _if the array is **special**, otherwise, return_ `-1`. It can be proven that if `nums` is special, the value for `x` is **unique**.

**Example 1:**

**Input:** nums = [3,5]
**Output:** 2
**Explanation:** There are 2 values (3 and 5) that are greater than or equal to 2.

**Example 2:**

**Input:** nums = [0,0]
**Output:** -1
**Explanation:** No numbers fit the criteria for x.
If x = 0, there should be 0 numbers >= x, but there are 2.
If x = 1, there should be 1 number >= x, but there are 0.
If x = 2, there should be 2 numbers >= x, but there are 0.
x cannot be greater since there are only 2 numbers in nums.

**Example 3:**

**Input:** nums = [0,4,3,0,4]
**Output:** 3
**Explanation:** There are 3 values that are greater than or equal to 3.

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

### Problem Analysis:

1. **High-Level Strategy**: 
    - The solution employs a binary search approach to find the special number, which is the number of elements in the array that are greater than or equal to the number itself.
    - The algorithm first sorts the input array `nums`, which is a prerequisite for binary search to work.
    - Then, it initializes two pointers, `l` and `r`, representing the left and right boundaries of the search range. Here, `l` starts at 0 and `r` at the length of the array `nums`.
    - The binary search iterates until `l` is less than or equal to `r`.
    - At each step, it calculates the `mid` point of the current range and counts the number of elements in `nums` greater than or equal to `mid`.
    - If the count matches the value of `mid`, it means `mid` is the special number, and it returns `mid`.
    - If the count is greater than `mid`, it means we need to search for a larger number, so it updates `l` to `mid + 1`.
    - If the count is less than `mid`, it means we need to search for a smaller number, so it updates `r` to `mid - 1`.
    - If no special number is found within the search range, the function returns -1.

2. **Complexity**:
    - Sorting the array initially takes O(n log n) time, where n is the length of the input array `nums`.
    - The binary search runs in O(log n) time.
    - Inside each binary search iteration, there's a call to `bisect.bisect_left(nums, mid)`, which takes O(log n) time as well.
    - Thus, the overall time complexity is O(n log n) due to the sorting step dominating.
    - The space complexity is O(1) since the algorithm uses only a constant amount of extra space for variables, and the sorting is done in-place.

## Solutions:

```python
class Solution:
    def specialArray(self, nums: List[int]) -> int:
        n = len(nums)
        l, r = 0, n

        nums.sort()
        while l<=r:
            mid = (l+r)//2
            count = n - bisect.bisect_left(nums, mid)
            if count == mid:
                return mid
            elif count > mid:
                l = mid + 1
            else:
                r = mid - 1
        return -1
```

## Similar Questions