---
last_reviewed: 2023-11-19
title: 1887 Reduce Operations to Make the Array Elements Equal - Medium
excerpt: "-"
tags:
  - solution
---
## Problem:
Given an integer array `nums`, your goal is to make all elements in `nums` equal. To complete one operation, follow these steps:

1. Find the **largest** value in `nums`. Let its index be `i` (**0-indexed**) and its value be `largest`. If there are multiple elements with the largest value, pick the smallest `i`.
2. Find the **next largest** value in `nums` **strictly smaller** than `largest`. Let its value be `nextLargest`.
3. Reduce `nums[i]` to `nextLargest`.

Return _the number of operations to make all elements in_ `nums` _equal_.

**Example 1:**

**Input:** nums = [5,1,3]
**Output:** 3
**Explanation:** It takes 3 operations to make all elements in nums equal:
1. largest = 5 at index 0. nextLargest = 3. Reduce nums[0] to 3. nums = [3,1,3].
2. largest = 3 at index 0. nextLargest = 1. Reduce nums[0] to 1. nums = [1,1,3].
3. largest = 3 at index 2. nextLargest = 1. Reduce nums[2] to 1. nums = [1,1,1].

**Example 2:**

**Input:** nums = [1,1,1]
**Output:** 0
**Explanation:** All elements in nums are already equal.

**Example 3:**

**Input:** nums = [1,1,2,2,3]
**Output:** 4
**Explanation:** It takes 4 operations to make all elements in nums equal:
1. largest = 3 at index 4. nextLargest = 2. Reduce nums[4] to 2. nums = [1,1,2,2,2].
2. largest = 2 at index 2. nextLargest = 1. Reduce nums[2] to 1. nums = [1,1,1,2,2].
3. largest = 2 at index 3. nextLargest = 1. Reduce nums[3] to 1. nums = [1,1,1,1,2].
4. largest = 2 at index 4. nextLargest = 1. Reduce nums[4] to 1. nums = [1,1,1,1,1].

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `1 <= nums[i] <= 5 * 104`

### Problem Analysis:
- **Counting Occurrences:**
    - The solution begins by creating a `Counter` object (`counter`) to efficiently count the occurrences of each unique element in the `nums` array.

- **Sorting Keys:**
    - The unique elements (keys) and their counts are extracted from the `counter` and sorted in descending order based on counts. This sorting is crucial for efficiently processing elements with higher counts first.

- **Accumulating Operations:**
    - The solution then iterates through the sorted keys, and for each key, it accumulates the count of that key in the `current` variable. The `current` variable represents the number of operations needed for the current key.

- **Total Operations:**
    - The `total` variable keeps track of the cumulative sum of the `current` variable for all keys except the last one. This total represents the minimum number of operations needed to make all array elements equal.
    
- **Result:**
    - The final result is the value stored in the `total` variable, which is the minimum number of operations required.


- **Time Complexity:**
    - O(N log N) due to the sorting operation.
        - The dominant factor in the time complexity is the sorting of the keys based on their counts. Sorting has a time complexity of O(N log N), where N is the length of the input array `nums`.
        
- **Space Complexity:**
    - O(N) for the `counter` and `keys` lists.
        - The `counter` dictionary and `keys` list store information about the unique elements and their counts. In the worst case, this space complexity is proportional to the size of the input array. The additional variables (`total` and `current`) use constant space.

## Solutions:

```python
class Solution:
    def reductionOperations(self, nums: List[int]) -> int:
        counter = collections.Counter(nums)
        keys = sorted(counter.keys(), reverse=True)
        
        total, current = 0, 0
        for key in keys[:-1]:
            current += counter[key]
            total += current
            
        return total        
```

## Similar Questions