---
last_reviewed: 2023-12-15
title: 1436 Destination City - Easy
excerpt: "-"
tags:
  - solution
---
## Problem:
You are given the array `paths`, where `paths[i] = [cityAi, cityBi]` means there exists a direct path going from `cityAi` to `cityBi`. _Return the destination city, that is, the city without any path outgoing to another city._

It is guaranteed that the graph of paths forms a line without any loop, therefore, there will be exactly one destination city.

**Example 1:**

**Input:** paths = `[["London","New York"],["New York","Lima"],["Lima","Sao Paulo"]]`
**Output:** "Sao Paulo" 
**Explanation:** Starting at "London" city you will reach "Sao Paulo" city which is the destination city. Your trip consist of: "London" -> "New York" -> "Lima" -> "Sao Paulo".

**Example 2:**

**Input:** paths = `[["B","C"],["D","B"],["C","A"]]`
**Output:** "A"
**Explanation:** All possible trips are: 
"D" -> "B" -> "C" -> "A". 
"B" -> "C" -> "A". 
"C" -> "A". 
"A". 
Clearly the destination city is "A".

**Example 3:**

**Input:** paths = `[["A","Z"]]`
**Output:** "Z"

**Constraints:**

- `1 <= paths.length <= 100`
- `paths[i].length == 2`
- `1 <= cityAi.length, cityBi.length <= 10`
- `cityAi != cityBi`
- All strings consist of lowercase and uppercase English letters and the space character.

### Problem Analysis:
- use a hashset to keep track of each start point
- iterate through the hashset and find the destination not in the set
- Time Complexity: O(n) where n is the number of paths
- Space Complexity: O(n)

## Solutions:

```python
class Solution:
    def destCity(self, paths: List[List[str]]) -> str:
        # similar to linked list
        s = set()
        for p in paths:
            s.add(p[0])
        
        for p in paths:
            if p[1] not in s:
                return p[1]
```

## Similar Questions