---
id: traveling-salesperson
aliases:
  - Traveling salesperson
  - traveling-salesperson
tags:
  - algorithm
---

# Traveling salesperson

Imagine a salesman that travels from city to city, selling his good. He wants to pick the shortest path that visits each city. If he wants to visit 5 cities, there are 120 possible ways to travel between each city, visiting each city once. For 6 cities, it will take 720 operations. For each city added, the number of permutations increases by a large number.

This is an example of the classic traveling salesperson problem. Scientists believe that it is not possible to optimize this problem.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

The traveling salesperson algorithm takes $O(n!)$ (factorial) time.
