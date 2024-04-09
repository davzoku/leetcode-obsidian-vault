---
last_reviewed: 2024-04-08
title: 1700 Number of Students Unable to Eat Lucnch
excerpt: "-"
tags:
  - solution
  - counter
  - stack
  - queue
---
## Problem:
The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers `0` and `1` respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a **stack**. At each step:

- If the student at the front of the queue **prefers** the sandwich on the top of the stack, they will **take it** and leave the queue.
- Otherwise, they will **leave it** and go to the queue's end.

This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays `students` and `sandwiches` where `sandwiches[i]` is the type of the `i​​​​​​th` sandwich in the stack (`i = 0` is the top of the stack) and `students[j]` is the preference of the `j​​​​​​th` student in the initial queue (`j = 0` is the front of the queue). Return _the number of students that are unable to eat._

**Example 1:**

**Input:** students = [1,1,0,0], sandwiches = [0,1,0,1]
**Output:** 0 
**Explanation:**
- Front student leaves the top sandwich and returns to the end of the line making students = [1,0,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,0,1,1].
- Front student takes the top sandwich and leaves the line making students = [0,1,1] and sandwiches = [1,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [1,1,0].
- Front student takes the top sandwich and leaves the line making students = [1,0] and sandwiches = [0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,1].
- Front student takes the top sandwich and leaves the line making students = [1] and sandwiches = [1].
- Front student takes the top sandwich and leaves the line making students = [] and sandwiches = [].
Hence all students are able to eat.

**Example 2:**

**Input:** students = [1,1,1,0,0,1], sandwiches = [1,0,0,0,1,1]
**Output:** 3

**Constraints:**

- `1 <= students.length, sandwiches.length <= 100`
- `students.length == sandwiches.length`
- `sandwiches[i]` is `0` or `1`.
- `students[i]` is `0` or `1`.

### Problem Analysis:
1. **High-Level Strategy**: 
    - The code utilizes a Counter object from the collections module to count the occurrences of each preference among the students.
    - It then iterates through the sandwiches one by one.
    - For each sandwich, it checks if there are students who prefer that type of sandwich available. If so, it decreases the count of that preference in the Counter.
    - If no students are left who prefer the current type of sandwich, it breaks out of the loop.
    - Finally, it returns the sum of the remaining values in the Counter, which represents the number of students who couldn't get their preferred sandwich.

2. **Complexity**:
    - Let's denote:
        - \( n \) as the number of students.
        - \( m \) as the number of sandwiches.
    - Constructing the Counter takes \( O(n) \) time.
    - The loop iterating through each sandwich has a complexity of \( O(m) \).
    - Within the loop, the operation of checking and decrementing the Counter takes \( O(1) \) time.
    - The final sum operation also takes \( O(n) \) time.
    - Thus, the overall time complexity is \( O(n + m) \). However, in the worst case, \( m \) could be equal to \( n \), so the complexity could be \( O(n^2) \).
    - The space complexity is \( O(n) \) due to the Counter object storing the preferences of students.

## Solutions:

```python
class Solution:
    def countStudents(self, students: List[int], sandwiches: List[int]) -> int:
        student_pref_counts = Counter(students)
        
        for sandwich in sandwiches:
            if student_pref_counts[sandwich] > 0:
                student_pref_counts[sandwich] -= 1
            else:
                break
        return sum(student_pref_counts.values())
```

## Similar Questions