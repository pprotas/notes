---
id: dijkstras-algorithm
aliases:
  - Dijkstra's algorithm
tags: []
---

# Dijkstra's algorithm

Dijkstra's algorithm is a [[algorithms#Greedy algorithms|greedy algorithm]] used for searching that runs on [[graphs#Weighted graphs|weighted graphs]]. It can answer what is the fastest path between two distinct nodes. Compare this to the [[breadth-first-search|breadth first search]], which can answer what is the path between two nodes with the least amount of edges.

Dijkstra's algorithm traverses all nodes in the graph to find the lowest amounts of weights it would take to visit each node, and through which parent node. You need to keep track of these weights and parents, and once all nodes have been traversed it's possible to backtrack from the target node to the root node through the parents to find the fastest path to the target node.

Let's say we have the following graph:

```python
graph = {
    "start": {"a": 6, "b": 3},
    "a": {"c": 1},
    "b": {"d": 6},
    "c": {"fin": 3, "e": 1},
    "d": {"fin": 3},
    "e": {"fin": 1},
    "fin": {},
}
```

What is the fastest way to get from `start` to `fin`? Breadth first search would come up with the path `start` -> `b` -> `d` -> `fin`. Even though this path has the least amount of vertices, it has the weight of 12. The fastest path is `start` -> `a` -> `c` -> `e` -> `fin`, which has the weight of 9. How does Dijkstra's algorithm find this path?

First, we need to keep track of the cheapest path to each node, and the parent node that leads to this cheapest path.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a`                | 6      | `start` |
| `b`                | 3      | `start` |
| `c`                |        |         |
| `d`                |        |         |
| `e`                |        |         |
| `fin`              |        |         |

We don't know the weights and parents of `c`, `d`, `e` and `fin` yet, since we haven't visited them yet. Dijkstra's algorithm will visit all nodes in the graph, and process them as follows:

1. Find the node with the smallest weight that you have not visited yet.
2. Look at the neighbors of this node. If you add the current node's weight from the table to the neighbor's weight, is it smaller than the current weight of the neighbor in the table? If yes, update the weight and the parent of the neighbor in the table.
3. Repeat from step 1 for every node in the graph
4. Backtrack through all the parents from `fin` to `start` in the table above to find the fastest path.

Let's go through the example graph step by step, keeping track of the state of the table at each step. We start at node `start`, which has the parents `a:6` and `b:3`. The table already contains this information.

1. The node with the smallest weight is `b:3`.
2. The neighbor of this node is `d:6`. We don't know the distance to `d` yet, so $3 + 6 = 9$ is now the shortest distance, through parent `b`.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a`                | 6      | `start` |
| `b` (x)            | 3      | `start` |
| `c`                |        |         |
| `d`                | 9      | `b`     |
| `e`                |        |         |
| `fin`              |        |         |

1. The node with the smallest weight is `a:6`.
2. The neighbor of this node is `c`. We don't know any paths to `c` yet, so $6 + 1 = 7$ is now the shortest path to `c` through `a`.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a` (x)            | 6      | `start` |
| `b` (x)            | 3      | `start` |
| `c`                | 7      | `a`     |
| `d`                | 9      | `b`     |
| `e`                |        |         |
| `fin`              |        |         |

1. The node with the smallest weight is `c:7`.
2. The neighbors of this node are `fin:3` and `e:1`. We don't know any paths to `fin` or `e` yet, so $7 + 3 = 10$ is now the shortest path to `fin` through `c`, and $7 + 1 = 8$ is now the shortest path to `e` through `c`.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a` (x)            | 6      | `start` |
| `b` (x)            | 3      | `start` |
| `c` (x)            | 7      | `a`     |
| `d`                | 9      | `b`     |
| `e`                | 8      | `c`     |
| `fin`              | 10     | `c`     |

1. The node with the smallest weight is `e:8`.
2. The neighbor of this node is `fin:1`. The current path to `e` is 10 weight through `c`, but $8 + 1 = 9$ is faster, and is now the fastest path to `fin` through `e`.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a` (x)            | 6      | `start` |
| `b` (x)            | 3      | `start` |
| `c` (x)            | 7      | `a`     |
| `d`                | 9      | `b`     |
| `e` (x)            | 8      | `c`     |
| `fin`              | 9      | `e`     |

1. The last unvisited node (we don't need to look at the target node) is `d`.
2. The neighbor to `d` is `fin:3`, but it's slower than the current fastest path because $9 + 3 = 12$, which is slower than the current fastest path of 9. We don't update the table.

| Node (visited "x") | Weight | Parent  |
| ------------------ | ------ | ------- |
| `start` (x)        | 0      | `start` |
| `a` (x)            | 6      | `start` |
| `b` (x)            | 3      | `start` |
| `c` (x)            | 7      | `a`     |
| `d` (x)            | 9      | `b`     |
| `e` (x)            | 8      | `c`     |
| `fin`              | 9      | `e`     |

Now that we have visited every node (except the target node), we can backktrack from `fin` through each parent until we reach `start`. The path is `fin` -> `e` -> `c` -> `a` -> `start`. If you reverse this path, you now have the fastest path from `start` to `fin`, which has 9 weights.

## Negative weights

Dijkstra's algorithm does not work if there are edges with negative weights. This is because you can not change the weight of a node once it has been visited. If you do this, then backtracking through the parents will not find the actual fastest path. This is because Dijkstra's alogirthm assumes that once you visited a node, you've already found the shortest path to it.

> [!tip] Bellman-Ford algorithm
>
> There is an algorithm called the [[bellman-ford-algorithm|Bellman-Ford algorithm]] that can handle negative weights.

## Example implementation

This is a code example of Dijkstra's algoirthm in [[python|Python]].

```python
graph = {
    "start": {"a": 6, "b": 3},
    "a": {"c": 1},
    "b": {"d": 6},
    "c": {"fin": 3, "e": 1},
    "d": {"fin": 3},
    "e": {"fin": 1},
    "fin": {},
}

costs = {
    "start": {"cost": 0, "parent": None},
    "a": {"cost": float("inf"), "parent": None},
    "b": {"cost": float("inf"), "parent": None},
    "c": {"cost": float("inf"), "parent": None},
    "d": {"cost": float("inf"), "parent": None},
    "e": {"cost": float("inf"), "parent": None},
    "fin": {"cost": float("inf"), "parent": None},
}

processed = set()  # a set is implemented ushing hash tables, so it's efficient for writing/reading processed nodes


def fastest_path(target):
    while len(processed) != len(graph) - 1:  # stop when every node is processed
        current_node = min(  # get smallest by weight unprocessed node
            [cost for cost in costs if cost not in processed],
            key=lambda node: costs[node]["cost"],
            default=None,
        )
        # prevent infnite loops with disconnected graphs or nodes with no outgoing edges
        if current_node is None:
            return "no path"

        cost = costs[current_node]["cost"]
        neighbors = graph[current_node]

        for n in neighbors.keys():  # check all neighbors
            # new cost is equal to the current cost and the edge from current_node to the neighbor
            new_cost = cost + neighbors[n]
            # only update the table if the new cost is actually lower
            if costs[n]["cost"] > new_cost:
                costs[n]["cost"] = new_cost
                costs[n]["parent"] = current_node
            # mark the node as processed
            processed.add(current_node)

    return backtrack_parent(target, [target])


# recursively go through the parents from the table, starting at the target node until you hit the root node
# then reverse the result
def backtrack_parent(node, path):
    if costs[node]["parent"] is None:
        path.reverse()
        return path
    path += [costs[node]["parent"]]
    return backtrack_parent(costs[node]["parent"], path)
```
