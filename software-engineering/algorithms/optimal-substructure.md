---
id: optimal-substructure
aliases:
  - Optimal substructure
tags: []
---

# Optimal substructure

A problem is said to have optimal substructure if an optimal solution can be found by the combination of optimal solutions to its subproblems. This property is important for [[greedy-algorithms|greedy algorithms]] and [[dynamic-programming|dynamic programming]].

Examples of problems with optimal substructure are [[dijkstras-algorithm|Dijkstra's algorithm]], where the shortest path (the problem) is a combination of the shortest paths to the nodes (the subproblems) that lead to the target node, and [[fibonacci-sequence|computing the Fibonacci sequence]], where the solution to the $n\text{th}$ number in the sequence (the problem) is the sum of the solutions to the $n-1\text{th}$ and $n-2\text{th}$ numbers (the subproblems) in the sequence.
