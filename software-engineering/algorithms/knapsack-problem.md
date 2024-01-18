---
id: knapsack-problem
aliases:
  - Knapsack problem
tags: []
---

# Knapsack problem

The knapsack problem describes the problem of fitting as many items as possible into a bag, taking into account the value of the items. It is an example of a problem that can be [[algorithms#Approximation algorithms|approximated]] with a [[greedy-algorithms|greedy algorithm]], although the greedy algorithm will not always find the optimal solution. The optimal solution to the problem can be found by using [[dynamic-programming|dynamic programming]].

## Greedy approach

For this example, these are the possible items that can be put into the bag:

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

## Dynamic programming approach

This problem is fitting for dynamic programming because you have to calculate the max value for each weight to be able to calculate the max value for the max weight ([[optimal-substructure|optimal substructure]]), and you have to calculate the max value for a given weight multiple times ([[overlapping-subproblems|overlapping subproblems]]). Since both criteria of dynamic programming are met, you can use it to solve the problem.

The dynamic programming approach for this problem looks like this:

1. Create a table with the weights as the columns and the items as the rows. The weights go from the minimum possible weight (the lightest item) to the maximum possible weight (the weight limit of the bag).
2. Start at the first item that you have not processed yet. At each row, you can only put in the items at that row or the row above it.
3. For each weight, calculate what the maximum value is that can be put in the bag and store it. The maximum value for a specific cell is either the value of the row above it (the previously found maximum), or the value of the current item combined with the value of the remaining space, whichever of the two is larger.
4. Repeat from step 2 until you have processed all items.
5. The value in the last row at the last column is the maximum value that can fit in the knapsack.

At step 3, the maximum value calculation for a specific cell looks like this in [[python|Python]], where `i` is the item index and `j` is the weight:

```python
previous_max = cell[i - 1][j]  # the maximum value of the cell above the current cell

# how much value can be put in the remaining space?
# this is already calculated in the previous iteration
remaining_space_value = cell[i - 1][j - item_weight]

cell[i][j] = max(
    cell[i - 1][j], item_value + remaining_space_value
)  # whichever one is bigger will be the maximum value for this cell
```

Let's say that these are the possible items that can be put into the bag:

| Item     | Weight | Value |
| -------- | ------ | ----- |
| Computer | 4kg    | $3000 |
| Laptop   | 3kg    | $2000 |
| Guitar   | 1kg    | $1500 |

This is how the solution to the problem would look like using dynamic programming:

```python
capacity = 4

values = [1500, 3000, 2000, 2000, 1000]
weights = [1, 4, 3, 1, 1]

# create a table like so;
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# the extra row and column is necessary to account for the situation where you look at the row above the first row
# think about it, there needs to be a way to look up, and then scan to the left
table = [[0] * (capacity + 1) for _ in range(len(values) + 1)]

# for each item (row), ignoring the first empty row
for i in range(1, len(values) + 1):
    # for each weight (column), ignoring the first empty column
    for j in range(1, capacity + 1):
        # get the current item from the array
        # the array is 0-indexed and our iterations are not, so need to decrement i by 1
        value = values[i - 1]
        weight = weights[i - 1]

        # the previous max is at the same column (j), but the row above it (i - 1)
        previous_max = table[i - 1][j]

        if weight > j:  # item does not fit in current cell
            table[i][j] = previous_max  # so previous max is still the best value
        else:  # item fits in the current cell
            # if there is any remaining space after we decrement the weight of the item, how much is it worth?
            remaining_space = table[i - 1][j - weight]

            table[i][j] = max(value, remaining_space + value)

# prints a table like so:
# [0,    0,    0,    0,    0]
# [0, 1500, 1500, 1500, 1500]
# [0, 1500, 1500, 1500, 3000]
# [0, 1500, 1500, 2000, 3500]
# [0, 2000, 3500, 3500, 4000]
# [0, 1000, 3000, 4500, 4500]
for row in table:
    print(row)

# prints the last cell, which is the last column of the last row (4500)
print(table[-1][-1])
```

This approach shows that the maximum value that can be put in the knapsack is $4500, which is the optimal solution.

It's important to note some important details and caveats for the dynamic programming approach. First of all, dynamic programming algorithms require for the problem to be discrete: the subproblems can not depend on each other. You might think that in the case of the knapsack problem the subproblems are not discrete, because the value of the current subproblem depends on the value of the previous subproblem. This is true, but that is not the definition of _discrete_. The term "discrete" means that the calculation of one subproblem does not lead to the changing of another subproblem. For example, let's say that we weren't talking about items to put in your bag, but about sights to see when planning a vacation trip. If two of your sights require for you to travel to Paris, you wouldn't count the travel time twice. This means that traveling to one of the sights would decrease the time for a different sight. This means that the subproblems are not discrete, because the calculation of one subproblem leads to the changing of another subproblem. This is not the case with the knapsack problem, because the calculation of one subproblem does not lead to the changing of another subproblem.

An important caveat is that the dynamic approach can not handle fractions. It is not possible to take half an item. Luckily, a greedy approach can handle fractions and results in the optimal solution.
