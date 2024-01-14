---
id: class-scheduling-problem
aliases:
  - Class scheduling problem
tags: []
---

# Class scheduling problem

The class scheduling problem describes the problem of fitting as many classes into a classroom as possible. It is an example of a problem that can be solved by a [[greedy-algorithms|greedy algorithm]].

Let's say that these are the possible classes that can be scheduled:

| Class | Start time | End time |
| ----- | ---------- | -------- |
| Art   | 9 AM       | 10AM     |
| Eng   | 9:30AM     | 10:30AM  |
| Math  | 10AM       | 11AM     |
| CS    | 10:30AM    | 11:30AM  |
| Music | 11AM       | 12PM     |

It is not possible to schedule two classes in this room at the same time, because there can only be one class in a room at a time. Also, it is not possible to schedule all classes because some of them overlap.

To find out how to schedule as many classes as possible you can use a greedy algorithm:

1. Pick the class that **ends the soonest**. This is the first class you'll hold in this classroom.
2. Pick the class that **starts after the first class** and also **ends the soonest**. This is the next class you'll hold in this classroom.
3. Repeat from step 2 until there are no classes left.

By following this algorithm, you will end up with the following schedule:

| Class | Start time | End time |
| ----- | ---------- | -------- |
| Art   | 9 AM       | 10AM     |
| Math  | 10AM       | 11AM     |
| Music | 11AM       | 12PM     |

This is the optimal schedule, because it is not possible to fit more classes into the classroom. The greedy algorithm will always find the optimal solution for this problem.
