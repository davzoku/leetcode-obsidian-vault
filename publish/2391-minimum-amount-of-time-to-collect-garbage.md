---
last_reviewed: 2023-11-20
title: 2391 Minimum Amount of Time to Collect Garbage - Medium
excerpt: "-"
tags:
  - solution
  - arrays
  - prefix-sum
---
## Problem:
You are given a **0-indexed** array of strings `garbage` where `garbage[i]` represents the assortment of garbage at the `ith` house. `garbage[i]` consists only of the characters `'M'`, `'P'` and `'G'` representing one unit of metal, paper and glass garbage respectively. Picking up **one** unit of any type of garbage takes `1` minute.

You are also given a **0-indexed** integer array `travel` where `travel[i]` is the number of minutes needed to go from house `i` to house `i + 1`.

There are three garbage trucks in the city, each responsible for picking up one type of garbage. Each garbage truck starts at house `0` and must visit each house **in order**; however, they do **not** need to visit every house.

Only **one** garbage truck may be used at any given moment. While one truck is driving or picking up garbage, the other two trucks **cannot** do anything.

Return _the **minimum** number of minutes needed to pick up all the garbage._

**Example 1:**

**Input:** garbage = ["G","P","GP","GG"], travel = [2,4,3]
**Output:** 21
**Explanation:**
The paper garbage truck:
1. Travels from house 0 to house 1
2. Collects the paper garbage at house 1
3. Travels from house 1 to house 2
4. Collects the paper garbage at house 2
Altogether, it takes 8 minutes to pick up all the paper garbage.
The glass garbage truck:
1. Collects the glass garbage at house 0
2. Travels from house 0 to house 1
3. Travels from house 1 to house 2
4. Collects the glass garbage at house 2
5. Travels from house 2 to house 3
6. Collects the glass garbage at house 3
Altogether, it takes 13 minutes to pick up all the glass garbage.
Since there is no metal garbage, we do not need to consider the metal garbage truck.
Therefore, it takes a total of 8 + 13 = 21 minutes to collect all the garbage.

**Example 2:**

**Input:** garbage = ["MMM","PGM","GP"], travel = [3,10]
**Output:** 37
**Explanation:**
The metal garbage truck takes 7 minutes to pick up all the metal garbage.
The paper garbage truck takes 15 minutes to pick up all the paper garbage.
The glass garbage truck takes 15 minutes to pick up all the glass garbage.
It takes a total of 7 + 15 + 15 = 37 minutes to collect all the garbage.

**Constraints:**

- `2 <= garbage.length <= 105`
- `garbage[i]` consists of only the letters `'M'`, `'P'`, and `'G'`.
- `1 <= garbage[i].length <= 10`
- `travel.length == garbage.length - 1`
- `1 <= travel[i] <= 100`
### Problem Analysis:

- **For Each Type of Garbage:**
    - For each type of garbage, the function calculates the maximum amount of that type that can be collected along the path.
    - It iterates through each garbage station (element in the `garbage` list) and considers the amount of the current type of garbage at that station.

- **Dynamic Accumulation of Collected Garbage:**
    - While iterating through garbage stations, the function accumulates the amount of the current type of garbage dynamically.
    - It considers the travel distance to the current station and adds the count of the current type of garbage at that station.
    
- **Maximization of Collection for Each Type:**
    - For each type of garbage, the function keeps track of the maximum amount that can be collected by updating the `mx` variable.
    - The maximum amount is determined based on the dynamic accumulation considering both the current station's garbage count and travel distance.
    
- **Total Collection:**
    - The `total` variable accumulates the maximum amounts of Metal, Plastic, and Glass that can be collected along the entire path.

- **Time Complexity:**
    - O(N * M) where N is the number of garbage stations and M is the average length of garbage strings.
        - The function iterates through each garbage station (N iterations) and, for each station, counts the occurrences of each type of garbage in the string (M operations).
        
- **Space Complexity:**
    - O(1) (constant space).
        - The function uses a constant amount of additional space for variables (`total`, `N`, `current`, `mx`, `c`, `i`). The space complexity is not dependent on the input size.

## Solutions:

```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        total = 0
        N = len(garbage)

        for c in "MPG":
            # mx: max
            # calculate for first element
            mx = garbage[0].count(c)
            current = mx

            for i in range(1, N):
                # move to next element
                current += travel[i-1]
                if c in garbage[i]:
                    current += garbage[i].count(c)
                    mx = max(current, mx)
            total += mx
        return total
```

## Similar Questions