---
id: dynamic-programming
aliases:
  - Dynamic programming
tags: []
---

# Dynamic programming

Dynamic programming is an approach for solving problems using an [[algorithms|algorithm]]. Just like [[divide-and-conquer]], it is not an algorithm itself, but an algorithm paradigm. Dynamic programming involves breaking down the given problem into smaller, repetitive and _discrete_ subproblems, solving each of those subproblems and building up towards solving the big problem. Discrete means that the subproblems don't depend on each other. As you solve the subproblems, you cache their solutions. This is called _memoization_: the storing of a value for later use.

Dynamic programming is useful when the [[recursion|recursive]] approach leads to exponential [[big-o|time complexity]], or when a [[greedy-algorithms|greedy algorithm]] fails because it does not lead to an optimal solution. In those situations, dynamic programming often leads to an optimal solution that is achieved more efficiently. Areas where dynamic programming is useful are:

- Optimization - finding the minimum or maximum value, finding the shortest path
- Combinatorics - counting the number of ways to do something
- Probability/statistics - finding probabilities or expected values in complex scenarios

There are two key attributes that a problem must possess in order for dynamic programming to be a viable approach:

1. [[optimal-substructure|Optimal substructure]] - the optimal solution can be achieved from the combination of optimal solutions to its subproblems.
2. [[overlapping-subproblems|Overlapping subproblems]] - the same subproblems are seen over and over again.

Greedy algorithms also share this requirement for optimal substructure. The difference between greedy algorithms and dynamic programming is this second point. Greedy algorithms make locally optimal choices and then solve the subproblems that arise later, where dynamic programming solves these subproblems first and then combines them toward the optimal solution. These subproblems need to be repetitive and discrete in the case of dynamic programming. This means that you see the same subproblem over and over again, and that one subproblem does not depend on the result of another subproblem.

A good approach for dynamic programming would be to start out with a recursive solution and optimize from there:

1. Find a recursive solution
2. [[memoization|Memoize]] the solutions to the subproblems (make the problem _top-down_)
3. Make it iterative (_bottom-up_)
   1. If possible, optimize for space

After the recursive solution is found, apply memoization to cache the results of subproblems. This cached value is used when the same subproblems are encountered again. This is called the top-down approach because you start with the big problem and break it down into smaller subproblems. This is very inherently recursive, since you start with the full input and break it down into smaller subproblems until you reach the base case. This is very similar to D&C, but the difference here is that the subproblems are discrete and repetitive, so you can cache their solutions.

The bottom-up approach is to start with the subproblems and build up towards the big problem. This is often more efficient because you don't have the overhead of the recursive calls. The bottom-up approach is also called _tabulation_. This approach involves iteratively solving bigger and bigger subproblems until you reach the solution. The reason that the terms "tabular" or "tabulation" are used is because this approach involves storing these bigger and bigger subproblems in a table, and using these precomputed subproblems from the table to solve bigger problems. This "bottom-up" approach is the most characteristic aspect of dynamic programming.

If it is possible to optimize for space, it is often a good idea to do so. Optimizing for space basically means using as least memory as possible. This is often possible when you only need the results of the previous two subproblems, or when you only need the results of the previous $n$ subproblems. This is often the case with the Fibonacci sequence, where you only need the results of the previous two numbers in the sequence to compute the next number.

For a great example of dynamic programming, see the notes on the [[fibonacci-sequence|Fibonacci sequence]]. Other problems suited for dynamic programming include the [[coin-change-problem|coin change problem]], the [[knapsack-problem|knapsack problem]], [[longest-common-subsequence|longest common subsequence]], [[longest-increasing-sequence|longest increasing sequence]] and the [[levenstein-distance|Levenstein distance]].
