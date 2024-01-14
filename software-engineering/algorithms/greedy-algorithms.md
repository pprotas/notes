---
id: greedy-algorithms
aliases:
  - Greedy algorithms
tags: []
---

# Greedy algorithms

When an [[algorithms|algorithm]] is _greedy_, it means that at each step of the algorithm, it makes a choice that is optimal at that moment in time. Instead of looking ahead (which is not always easy or possible) to find the best possible solutions, it chooses the best possible solution at specific moments, with the intention that this will lead to the best possible solution overall. This does not always work, but it often does, and when it does it often leads to simple algorithms.

In a way, greedy algorithms give up the systematic approach and the guarantees that come with it, in the hopes that the algorithm finds a "good enough" solution in a more efficient manner. Look at a systemic, precise algorithm like [[breadth-first-search|BFS]]. BFS guarantees that it will find the shortest path in a graph, but it might be way too slow for huge graphs. It does this by working toward a predetermined final state: the target node is found. This is different from a greedy algorithm, which does not have a predetermined final state. Instead, it makes locally optimal choices and hopes that this will lead to the optimal solution overall.

An example of greedy algorithms is [[dijkstras-algorithm|Dijkstra's algorithm]]. At each step in the algorithm, it tries to find the fastest path to the target node in that moment in time without considering the overall structure of the graph. In the next step it attempts the same thing, and if the path is faster than the previous step, it will update the path. This continues until all nodes have been visited, and the fastest path to the target node has been found. There is no predetermined final state that this algorithm is trying to achieve. Instead, the algorithm makes a bunch of good choices and these good choices add up to the optimal solution.

Dijkstra's algorithm is special in that it is a greedy algorithm that **does** find the optimal solution. This is typically not the case. Just because the optimal solution is found, does not characterize the greediness of the algorithm - it does not say anything about whether the algorithm is greedy or not. When greedy algorithms are conjectured to find the optimal solution, they often become the method of choice due to the combination of lower complexity than the systematic approach, and the guarantee of finding the optimal solution. Another example that fits this criteria are the solutions to finding [[minimum-spanning-trees|minimum spanning trees]].

A different example of a problem that can be solved with a greedy algorithm is the [[class-scheduling-problem|class scheduling problem]].

> [!info]
>
> There are many algorithms that would be considered "non-greedy". These algorithms often fit into strategies like [[divide-and-conquer]] or [[dynamic-programming|dynamic programming]]. Algorithms that follow these strategies are not greedy, since they systematically approach the problem, instead of making locally optimal choices.

A problem needs to meet two criteria in order for a greedy algorithm to be a viable approach:

1. Greedy choice property - the algorithm does not reconsider its choices. The choices are made iteratively, one after another and there is never an attempt to backtrack.
2. [[optimal-substructure|Optimal substructure]] - the optimal solution (or its approximation) can be achieved from the combination of optimal solutions to its subproblems.

This first point is the main difference between greedy algorithms and [[dynamic-programming|dynamic programming]]. Dynamic programming solves the subproblems first, and then combines them toward the optimal solution. Greedy algorithms make locally optimal choices and then solve the subproblems that arise later.
