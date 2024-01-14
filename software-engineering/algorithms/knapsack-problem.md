---
id: knapsack-problem
aliases:
  - Knapsack problem
tags: []
---

# Knapsack problem

The knapsack problem describes the problem of fitting as many items as possible into a bag, taking into account the value of the items. It is an example of a problem that can be approached with a [[algorithms#Greedy algorithms|greedy algorithm]], although the greedy algorithm will not always find the optimal solution.

Let's say that these are the possible items that can be put into the bag:

| Item     | Weight | Value |
| -------- | ------ | ----- |
| Computer | 10kg   | $3000 |
| Laptop   | 5kg    | $2000 |
| Guitar   | 3kg    | $1500 |

Let's say that you can only fit 10kg of items into the bag. The greedy algorithm for this problem would be:

1. Pick the most expensive thing that will fit into the bag and put it in the bag.
2. Repeat until the bag is full.

By following this algorithm, you will only end up with the computer in your bag. This is not the optimal solution, because you could have put the laptop and the guitar in the bag, which would have been worth $3500.

Although the greedy solution is not optimal, it could still be considered pretty good (or _good enough_) in some situations.
