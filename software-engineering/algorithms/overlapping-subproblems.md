---
id: overlapping-subproblems
aliases:
  - Overlapping subproblems
tags: []
---

# Overlapping subproblems

Sometimes a problem can be approached by breaking it down into smaller subproblems. An example of this is [[quicksort]], where the problem of sorting an array is broken down into the problem of sorting two smaller arrays. The smaller arrays are then sorted, and combined to form the solution to the original problem. Every time you break down the array, you break it down into two smaller arrays. The same section of the array is never repeated.

On the other hand, there are problems where the subproblems overlap. In this context, _overlapping_ means that they repeat over and over again. An example of this is the [[fibonacci-sequence|Fibonacci sequence]], where the solution to the $n\text{th}$ number in the sequence is the sum of the solutions to the $(n-1)\text{th}$ and $(n-2)\text{th}$ numbers in the sequence. To solve the $n\text{th}$ number, you need to solve the $(n-1)\text{th}$, and to solve the $(n-1)\text{th}$ number, you need to solve the $(n-2)\text{th}$ number. Therefore, the computation of the $(n-2)\text{th}$ number is repeated twice. This is the key characteristic of overlapping subproblems: the same subproblem is seen over and over again.

[[dynamic-programming|Dynamic programming]] requires that the problem can be broken down into overlapping subproblems. A common approach with overlapping subproblems is to use [[memoization]], where you cache the solution to a subproblem for later use.
