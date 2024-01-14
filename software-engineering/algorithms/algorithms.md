---
id: algorithms
aliases:
  - Algorithms
tags: []
---

# Algorithms

An algorithm is a set of instructions for accomplishing a task. In theory, every piece of code that accomplishes a task is therefore an algorithm, but this is not what is often meant by the term. In the context of software engineering or computer science, people refer to "algorithms" as specialized pieces of code that are designed to efficiently solve a problem. This efficiency of an algorithm is often measured by its time and space complexity, expressed in [[big-o|Big O]] notation.

Different algorithms are useful for different problems. The same problem can also be solved by multiple algorithms. Choosing the right algorithm for a given problem is a key part of software engineering, and involves weighing the trade offs between the algorithms.

There are many algorithm paradigms, which are different approaches to writing algorithms. Take a look at [[greedy-algorithms|greedy algorithms]], [[divide-and-conquer|divide and conquer]] and [[dynamic-programming|dynamic programming]] for examples of different algorithm paradigms.

## Approximation algorithms

When calculating the exact solution takes too much time, an approximation algorithm can do the trick. Approximation algorithms are judged by how fast they are and how close they are to the optimal solution.

Greedy algorithms are often a good choice for approximation algorithms. The [[set-cover-problem|set cover problem]] and the [[knapsack-problem|knapsack problem]] are examples of problems that can be approximated with a greedy algorithm.
