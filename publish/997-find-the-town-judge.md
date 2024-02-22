---
last_reviewed: 2024-02-22
title: 
excerpt: "-"
tags:
  - solution
---
## Problem:
In a town, there are `n` people labeled from `1` to `n`. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

1. The town judge trusts nobody.
2. Everybody (except for the town judge) trusts the town judge.
3. There is exactly one person that satisfies properties **1** and **2**.

You are given an array `trust` where `trust[i] = [ai, bi]` representing that the person labeled `ai` trusts the person labeled `bi`. If a trust relationship does not exist in `trust` array, then such a trust relationship does not exist.

Return _the label of the town judge if the town judge exists and can be identified, or return_ `-1` _otherwise_.

**Example 1:**

**Input:** n = 2, trust = [[1,2]]
**Output:** 2

**Example 2:**

**Input:** n = 3, trust = [[1,3],[2,3]]
**Output:** 3

**Example 3:**

**Input:** n = 3, trust = [[1,3],[2,3],[3,1]]
**Output:** -1

**Constraints:**

- `1 <= n <= 1000`
- `0 <= trust.length <= 104`
- `trust[i].length == 2`
- All the pairs of `trust` are **unique**.
- `ai != bi`
- `1 <= ai, bi <= n`

### Problem Analysis:
1. **High-level Strategy**:
    - The solution first initializes a list `tracker` with `n` elements, all initialized to zero. This list will keep track of the net trust scores for each person.
    - Then, it iterates through the list of trusts. For each pair `(a, b)` in `trust`, it decrements the trust score of `a-1` and increments the trust score of `b-1`.
    - Finally, it iterates through the `tracker` list and checks if any person has a trust score of `n-1`. If found, it returns the index of that person plus one (to match the 1-based indexing used in the problem statement). If no such person is found, it returns `-1`.
2. **Complexity**:
    - **Time Complexity**:
        - The loop that iterates through the list of trusts runs in O(E), where E is the number of trust relationships.
        - The loop that iterates through the `tracker` list runs in O(N), where N is the number of people.
        - Thus, the overall time complexity is O(N + E).
    - **Space Complexity**:
        - The space complexity is O(N) because of the `tracker` list.

## Solutions:

```python
class Solution:
    def findJudge(self, n: int, trust: List[List[int]]) -> int:
        tracker = [0] * n


        for a,b in trust:
            tracker[a-1] -=1
            tracker[b-1] +=1

        # if town judge, trust == n-1, should match
        for i in range(0, n):
            if tracker[i] == n-1:
                return i+1
        return -1
```

## Similar Questions