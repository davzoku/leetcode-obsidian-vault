---
last_reviewed: 2023-12-06
title: 
excerpt: "-"
tags:
  - solution
  - math
  - arithmetic-progression
---
## Problem:
Hercy wants to save money for his first car. He puts money in the Leetcode bank **every day**.

He starts by putting in `$1` on Monday, the first day. Every day from Tuesday to Sunday, he will put in `$1` more than the day before. On every subsequent Monday, he will put in `$1` more than the **previous Monday**.

Given `n`, return _the total amount of money he will have in the Leetcode bank at the end of the_ `nth` _day._

**Example 1:**

**Input:** n = 4
**Output:** 10
**Explanation:** After the 4th day, the total is 1 + 2 + 3 + 4 = 10.

**Example 2:**

**Input:** n = 10
**Output:** 37
**Explanation:** After the 10th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4) = 37. Notice that on the 2nd Monday, Hercy only puts in $2.

**Example 3:**

**Input:** n = 20
**Output:** 96
**Explanation:** After the 20th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4 + 5 + 6 + 7 + 8) + (3 + 4 + 5 + 6 + 7 + 8) = 96.

**Constraints:**

- `1 <= n <= 1000`
### Problem Analysis:
- This question is an Arithmetic Progression problem, we need to be familiar with the Arithmetic Progression Formula List and apply it accordingly.

![[ap-formula-list.png]]

- Time Complexity: O(1)
- Space Complexity: O(1)

## Solutions:

```python
class Solution:
    def totalMoney(self, n: int) -> int:
        # w1 = 1+2+3+4+5+6+7 = 28
        # w2 = ... = 28 + 7
        # ap formula 1: Sn = n/2[2a + (n – 1)d]
        # ap formula 2: Sn = n/2[first term + last term]
        w = n // 7 # weeks
        rd = n % 7 # remaining days
        return w * 28 + 7 * (w - 1) * w // 2 + (w + 1 + w + rd) * rd // 2
```

## Similar Questions