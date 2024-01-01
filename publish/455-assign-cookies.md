---
last_reviewed: 2024-01-01
title: 
excerpt: "-"
tags:
  - solution
  - arrays
  - greedy
  - sorting
---
## Problem:
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child `i` has a greed factor `g[i]`, which is the minimum size of a cookie that the child will be content with; and each cookie `j` has a size `s[j]`. If `s[j] >= g[i]`, we can assign the cookie `j` to the child `i`, and the child `i` will be content. Your goal is to maximize the number of your content children and output the maximum number.

**Example 1:**

**Input:** g = [1,2,3], s = [1,1]
**Output:** 1
**Explanation:** You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.

**Example 2:**

**Input:** g = [1,2], s = [1,2,3]
**Output:** 2
**Explanation:** You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.

**Constraints:**

- `1 <= g.length <= 3 * 104`
- `0 <= s.length <= 3 * 104`
- `1 <= g[i], s[j] <= 231 - 1`

### Problem Analysis:

High-level strategy:

1. Sort the lists of greed factors (`g`) and cookie sizes (`s`) in ascending order.
2. Initialize pointers `i` and `j` to iterate through the greed factors and cookie sizes, respectively.
3. Iterate through the lists while comparing greed factors and cookie sizes.
4. If the current cookie size is sufficient to satisfy the current child, move to the next child and the next cookie.
5. Increment the count of satisfied children.
6. Finally, return the count of satisfied children.

Complexity:

- Time Complexity: O(max(N log N, M log M)), where N is the length of `g` and M is the length of `s`. This is due to the sorting of both lists.
- Space Complexity: O(1). The algorithm uses a constant amount of extra space.

## Solutions:

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()

        res = 0
        i, j = 0, 0

        while i < len(g) and j < len(s):
            # If the current cookie size is greater than or equal to the current child's greed factor
            # It means the child can be satisfied, move to the next child and next cookie
            if s[j] >= g[i]:
                res += 1
                i += 1
            j += 1

        return res
```

## Similar Questions