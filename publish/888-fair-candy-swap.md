---
last_reviewed: 2023-11-30
title: 888 Fair Candy Swap - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
Alice and Bob have a different total number of candies. You are given two integer arrays `aliceSizes` and `bobSizes` where `aliceSizes[i]` is the number of candies of the `ith` box of candy that Alice has and `bobSizes[j]` is the number of candies of the `jth` box of candy that Bob has.

Since they are friends, they would like to exchange one candy box each so that after the exchange, they both have the same total amount of candy. The total amount of candy a person has is the sum of the number of candies in each box they have.

Return a_n integer array_ `answer` _where_ `answer[0]` _is the number of candies in the box that Alice must exchange, and_ `answer[1]` _is the number of candies in the box that Bob must exchange_. If there are multiple answers, you may **return any** one of them. It is guaranteed that at least one answer exists.

**Example 1:**

**Input:** aliceSizes = [1,1], bobSizes = [2,2]
**Output:** [1,2]

**Example 2:**

**Input:** aliceSizes = [1,2], bobSizes = [2,3]
**Output:** [1,2]

**Example 3:**

**Input:** aliceSizes = [2], bobSizes = [1,3]
**Output:** [2,3]

**Constraints:**

- `1 <= aliceSizes.length, bobSizes.length <= 104`
- `1 <= aliceSizes[i], bobSizes[j] <= 105`
- Alice and Bob have a different total number of candies.
- There will be at least one valid answer for the given input.
### Problem Analysis:
- Each element in the array is a candy box, and both Alice and Bob have to swap 1 candy box to make the number of candies each person has equal
- Find the target sum that each person should have
- for each Alice's candy box, try to find a Bob's candy box that can be swapped such that, the final sum of candies for each person is the same

- Time complexity: O(A+B)
- Space complexity: O(B)
## Solutions:

```python
class Solution:
    def fairCandySwap(self, aliceSizes: List[int], bobSizes: List[int]) -> List[int]:
        sumA, sumB = sum(aliceSizes), sum(bobSizes)
        target_sum = (sumA + sumB) // 2
        # for lookup
        setB = set(bobSizes)

        for sizeA in aliceSizes:
            sizeB_expected = target_sum - (sumA - sizeA)
            if sizeB_expected in setB:
                return [sizeA, sizeB_expected]
```

## Similar Questions