---
last_reviewed: 2024-07-22
title: 2418 Sort the People - Easy
excerpt: "-"
tags:
  - solution
  - arrays
---
## Problem:
You are given an array of strings `names`, and an array `heights` that consists of **distinct** positive integers. Both arrays are of length `n`.

For each index `i`, `names[i]` and `heights[i]` denote the name and height of the `ith` person.

Return `names` _sorted in **descending** order by the people's heights_.

**Example 1:**

**Input:** names = ["Mary","John","Emma"], heights = [180,165,170]
**Output:** ["Mary","Emma","John"]
**Explanation:** Mary is the tallest, followed by Emma and John.

**Example 2:**

**Input:** names = ["Alice","Bob","Bob"], heights = [155,185,150]
**Output:** ["Bob","Alice","Bob"]
**Explanation:** The first Bob is the tallest, followed by Alice and the second Bob.

**Constraints:**

- `n == names.length == heights.length`
- `1 <= n <= 103`
- `1 <= names[i].length <= 20`
- `1 <= heights[i] <= 105`
- `names[i]` consists of lower and upper case English letters.
- All the values of `heights` are distinct.

### Problem Analysis:
### 1. High-Level Strategy

The solution follows a straightforward approach to sort people based on their heights:

1. **Zipping**: Combine the `names` and `heights` lists into a list of tuples, where each tuple contains a name and the corresponding height.

2. **Sorting**: Sort these tuples based on the height in descending order. This is done using the `sorted` function with a custom key (`lambda x: x[1]`) to sort by the height values, and `reverse=True` to ensure the order is from tallest to shortest.

3. **Extracting Names**: After sorting, extract just the names from the sorted list of tuples. This is achieved using a list comprehension that iterates over the sorted tuples and collects the names.

This approach is effective for problems where you need to sort a collection based on one of its elements and then extract a specific part of the sorted result.

### 2. Complexity

**Time Complexity**:
- **Zipping**: The `zip` function runs in O(n) time, where n is the number of elements in the input lists.
- **Sorting**: The `sorted` function has a time complexity of O(n log n), where n is the number of elements being sorted.
- **Extracting Names**: The list comprehension runs in O(n) time to extract names from the sorted list of tuples.

Overall, the dominant term in the time complexity is the sorting step, so the overall time complexity of the solution is **O(n log n)**.

**Space Complexity**:
- **Space for Zipped List**: The space used for the zipped list of tuples is O(n).
- **Space for Sorted List**: The sorted list of tuples also takes O(n) space.
- **Space for Result List**: The list of extracted names takes O(n) space.

Thus, the space complexity of the solution is **O(n)**, primarily due to the storage requirements for the zipped, sorted, and result lists.

## Solutions:

```python
class Solution:
    def sortPeople(self, names: List[str], heights: List[int]) -> List[str]:
        zipped = zip(names, heights)
        sorted_zipped = sorted(zipped, key=lambda x: x[1], reverse=True)
        return [name for name, height in sorted_zipped]
```

## Similar Questions