---
last_reviewed: 2024-04-09
title: 2073 Time Needed to Buy Tickets - Easy
excerpt: "-"
tags:
  - solution
  - arrays
---
## Problem:
There are `n` people in a line queuing to buy tickets, where the `0th` person is at the **front** of the line and the `(n - 1)th` person is at the **back** of the line.

You are given a **0-indexed** integer array `tickets` of length `n` where the number of tickets that the `ith` person would like to buy is `tickets[i]`.

Each person takes **exactly 1 second** to buy a ticket. A person can only buy **1 ticket at a time** and has to go back to **the end** of the line (which happens **instantaneously**) in order to buy more tickets. If a person does not have any tickets left to buy, the person will **leave** the line.

Return _the **time taken** for the person at position_ `k` **_(0-indexed)_** _to finish buying tickets_.

**Example 1:**

**Input:** tickets = [2,3,2], k = 2
**Output:** 6
**Explanation:** 
- In the first pass, everyone in the line buys a ticket and the line becomes [1, 2, 1].
- In the second pass, everyone in the line buys a ticket and the line becomes [0, 1, 0].
The person at position 2 has successfully bought 2 tickets and it took 3 + 3 = 6 seconds.

**Example 2:**

**Input:** tickets = [5,1,1,1], k = 0
**Output:** 8
**Explanation:**
- In the first pass, everyone in the line buys a ticket and the line becomes [4, 0, 0, 0].
- In the next 4 passes, only the person in position 0 is buying tickets.
The person at position 0 has successfully bought 5 tickets and it took 4 + 1 + 1 + 1 + 1 = 8 seconds.

**Constraints:**

- `n == tickets.length`
- `1 <= n <= 100`
- `1 <= tickets[i] <= 100`
- `0 <= k < n`

### Problem Analysis:
1. **High-level strategy**:

    - The function `timeRequiredToBuy` aims to calculate the total time needed to buy all tickets. It considers buying tickets in a specific order denoted by the index `k`.
    - The approach calculates the time needed to buy tickets sequentially, starting from the `k`-th ticket, and then considering the remaining tickets either forward or backward depending on their position relative to `k`.
    - It iterates through the tickets, calculating the time needed to buy each ticket and accumulating it to the total time.

1. **Complexity Analysis**:
    - Let `n` be the number of tickets.
    - The time complexity of this solution is O(n) because it iterates through the list of tickets once.
    - Within the loop, the operations are mostly constant time, such as comparison and addition.
    - Thus, the overall time complexity of the solution is O(n).

## Solutions:

```python
class Solution:
    def timeRequiredToBuy(self, tickets: List[int], k: int) -> int:
        output = tickets[k]
        others = 0
        inter = 0
        for i, t in enumerate(tickets):
            if i != k:
                inter = min(t, output)
                if i > k and inter == output:
                    inter-=1
                others += inter
        
        return output+others
```

## Similar Questions