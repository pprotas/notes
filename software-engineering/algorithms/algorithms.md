---
id: algorithms
aliases:
  - Algorithms
tags: []
---

# Algorithms

An algorithm is a set of instructions for accomplishing a task. In theory, every piece of code that accomplishes a task is therefore an algorithm, but this is not what is often meant by the term. In the context of software engineering or computer science, people refer to "algorithms" as specialized pieces of code that are designed to efficiently solve a problem. This efficiency of an algorithm is often measured by its time and space complexity, expressed in [[big-o|Big O]] notation.

Different algorithms are useful for different problems. The same problem can also be solved by multiple algorithms. Choosing the right algorithm for a given problem is a key part of software engineering, and involves weighing the trade offs between the algorithms.

## Greedy algorithms

When an algorithm is _greedy_, it means that at each step of the algorithm, it makes a choice that is optimal at that moment in time. Instead of looking ahead (which is not always easy or possible) to find the best possible solutions, it chooses the best possible solution at specific moments, with the intention that this will lead to the best possible solution overall. This does not always work, but it often does, and when it does it often leads to simple algorithms.

In a way, greedy algorithms give up the systematic approach and the guarantees that come with it, in the hopes that the algorithm finds a "good enough" solution in a more efficient manner. Look at a systemic, precise algorithm like [[breadth-first-search|BFS]]. BFS guarantees that it will find the shortest path in a graph, but it might be way too slow for huge graphs. A greedy algorithm would sacrifice the guarantee of BFS and only search some nodes based on some heuristic or assumption that aims for a locally optimal choice at each step, but it might find **one of** the shortest paths in a big graph in a realistic time frame. This adaptation would involve selecting nodes based on criteria believed to lead more directly or quickly to a solution, rather than systematically exploring all nodes at a given depth.

An example of greedy algorithms is [[dijkstras-algorithm|Dijkstra's algorithm]]. At each step in the algorithm, it tries to find the fastest path to the target node in that moment in time without considering the overall structure of the graph. In the next step it attempts the same thing, and if the path is faster than the previous step, it will update the path. This continues until all nodes have been visited, and the fastest path to the target node has been found. Compare this to a greedy algorithm that might attempt to find the shortest path by looking at every node and looking at every possible path that can lead to another nodes, then choosing the path with the lowest weight. You can see how this approach is more systematic, but the greedy Dijkstra algorithm is much faster.

Dijkstra's algorithm is special in that it is a greedy algorithm that **does** find the optimal solution. This is typically not the case. Just because the optimal solution is found, does not characterize the greediness of the algorithm - it does not say anything about whether the algorithm is greedy or not. When greedy algorithms are conjectured to find the optimal solution, they often become the method of choice due to the combination of lower complexity than the systematic approach, and the guarantee of finding the optimal solution. Another example that fits this criteria are the solutions to finding [[minimum-spanning-trees|minimum spanning trees]].

A different example of a problem that can be solved with a greedy algorithm is the [[class-scheduling-problem|class scheduling problem]].

> [!info]
>
> There are many algorithms that would be considered "non-greedy". These algorithms often fit into strategies like [[divide-and-conquer]] or [[dynamic-programming|dynamic programming]]. Algorithms that follow these strategies are not greedy, since they systematically approach the problem, instead of making locally optimal choices.

## Approximation algorithms

When calculating the exact solution takes too much time, an approximation algorithm can do the trick. Approximation algorithms are judged by how fast they are and how close they are to the optimal solution.

Greedy algorithms are often a good choice for approximation algorithms. The [[set-cover-problem|set cover problem]] and the [[knapsack-problem|knapsack problem]] are examples of problems that can be approximated with a greedy algorithm.
