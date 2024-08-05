---
last_reviewed: 2024-08-05
title: 2053 Kth Distinct String in an Array - Easy
excerpt: "-"
tags:
  - solution
  - arrays
  - hashmap
---
## Problem:
A **distinct string** is a string that is present only **once** in an array.

Given an array of strings `arr`, and an integer `k`, return _the_ `kth` _**distinct string** present in_ `arr`. If there are **fewer** than `k` distinct strings, return _an **empty string**_ `""`.

Note that the strings are considered in the **order in which they appear** in the array.

**Example 1:**

**Input:** arr = ["d","b","c","b","c","a"], k = 2
**Output:** "a"
**Explanation:**
The only distinct strings in arr are "d" and "a".
"d" appears 1st, so it is the 1st distinct string.
"a" appears 2nd, so it is the 2nd distinct string.
Since k == 2, "a" is returned. 

**Example 2:**

**Input:** arr = ["aaa","aa","a"], k = 1
**Output:** "aaa"
**Explanation:**
All strings in arr are distinct, so the 1st string "aaa" is returned.

**Example 3:**

**Input:** arr = ["a","b","a"], k = 3
**Output:** ""
**Explanation:**
The only distinct string is "b". Since there are fewer than 3 distinct strings, we return an empty string "".

**Constraints:**

- `1 <= k <= arr.length <= 1000`
- `1 <= arr[i].length <= 5`
- `arr[i]` consists of lowercase English letters.

### Problem Analysis:
Sure, let's break down the solution to the LeetCode problem step by step.

### 1. High-Level Strategy

The high-level strategy of this solution involves the following steps:

1. **Count Occurrences**: Use a `Counter` from the `collections` module to count the occurrences of each string in the array.
2. **Filter Distinct Strings**: Iterate through the array to collect all strings that appear exactly once into a new list `distinct`.
3. **Select the k-th Distinct String**: Check if there are at least `k` distinct strings. If so, set the output to the `k-th` distinct string (considering 1-based index), otherwise, return an empty string.

### 2. Complexity

#### Time Complexity

1. **Counting Occurrences**: The `Counter` creation involves a single pass through the array, which takes \( O(n) \) time, where \( n \) is the length of the array.
2. **Filtering Distinct Strings**: The iteration through the array to collect distinct strings also takes \( O(n) \) time.
3. **Checking and Retrieving the k-th Element**: Checking the length of the `distinct` list and retrieving the `k-th` element, if present, is \( O(1) \).

Overall, the time complexity is \( O(n) \).

#### Space Complexity

1. **Counter Storage**: The `Counter` stores each unique string and its count, which in the worst case takes \( O(n) \) space if all strings are unique.
2. **Distinct List Storage**: The `distinct` list stores all distinct strings, which in the worst case could also take \( O(n) \) space if all strings appear exactly once.

Therefore, the overall space complexity is \( O(n) \).

### Summary

- **High-Level Strategy**: The solution counts the occurrences of each string, filters out the distinct strings, and returns the k-th distinct string if it exists.
- **Time Complexity**: \( O(n) \)
- **Space Complexity**: \( O(n) \)

This approach ensures that the solution is efficient both in terms of time and space, making it suitable for large inputs within the typical constraints of such problems.

## Solutions:

```python
class Solution:
    def kthDistinct(self, arr: List[str], k: int) -> str:
        counter = Counter(arr)
        distinct = []
        output = ""
        for i in arr:
            if counter.get(i) == 1:
                distinct.append(i)
        if len(distinct) >= k:
            output = distinct[k-1]

        return  output
```

## Similar Questions