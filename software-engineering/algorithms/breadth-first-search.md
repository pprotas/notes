---
id: breadth-first-search
aliases:
  - Breadth-first search
tags: []
---

# Breadth-first search

Breadth-first search is a search [[algorithms|algorithm]] that runs on [[graphs]]. It can answer whether there is a path between two distinct nodes, and what is the shortest path between them. The name of the algorithm comes from the fact that the algorithm searches the graph layer by layer, starting at the root node.

> [!note] The shortest path
>
> The "shortest path" refers to the path that contains the least amount of edges. The shortest path is not always the fastest path. In the context of [[graphs#Weighted graphs|weighted graphs]], the fastest path is not necessearily the path with the least amount of edges, but the path with the least amount of total weight. [[dijkstras-algorithm|Dijkstra's algorithm]] is a good fit for finding the fastest path in a weighted graph.

The core of the algorithm is that you start at the root node, and visit all of its neighbors. If none of the neighbors are the node you're searching for, you visit the neighbors of the neighbors. This continues until you find the desired node, or you run out of nodes to visit. Because of the breadth-first approach, the shortest path is also the very first path that is found, since the algorithm starts at the root node and works its way outwards

You can imagine looking for a specific person in your social network. You start with all of your 1st degree connections, and if that person is not found, you continue on to the 2nd degree connections - the friends of your friends. You continue on until you find the person you're looking for. The degree at which you find this person is the lowest possible degree, and thus the shortest path.

This approach of searching layer by layer is very fitting for [[queues]]. This is because each layer needs to be handled in the order that it was discovered.

## Example implementation

The summary of the workings of the algorithms:

1. Keep a queue containing the nodes to check
2. Pop a node from the queue
3. Check if this is the target nodes
   1. If yes, return this node (algorithm is finished)
   2. If no, add all neighbors of this node to the queue
4. Repeat from step 2 until the queue is empty or the target is found
5. If the queue is empty, there is no path to the target node

Here's an example implementation of the breadth-first search algorithm in [[python|Python]]:

```python
from collections import deque


graph = {}
graph["you"] = ["alice", "bob", "claire"]
graph["bob"] = ["anuj", "peggy"]
graph["alice"] = ["peggy"]
graph["claire"] = ["thom", "jonny"]
graph["anuj"] = []
graph["peggy"] = []
graph["thom"] = []
graph["jonny"] = []


def breadth_first_search(graph, target):
    search_queue = deque()
    search_queue += graph["you"]  # start at the root node

    while search_queue:
        person = search_queue.popleft()
        if person == target:
            return True
        else:
            search_queue += graph[person]
    return False


print(breadth_first_search(graph, "thom")) # True
print(breadth_first_search(graph, "paewl")) # False
```

The function prints `True` if there is a path from the root node to the target, and `False` if there is no path. There is one problem with this implementation, it's possible that it will check the same node multiple times. This is a mistake because there is no need to check a node again if it's already been checked, since the result will be the same no matter how many times you check a node. On top of that, this can lead to an infinite loop if two nodes reference each other, like this:

```python
graph = {}
graph["bob"] = ["alice"]
graph["alice"] = ["bob"]
```

The solution is to keep track of the nodes that have already been checked. A hash table is a good fit for this task, since it can store and read in $O(1)$ time. Here's an example implementation:

```python
def breadth_first_search(graph, target):
    search_queue = deque()
    search_queue += graph["you"]  # start at the root node

    searched = {}

    while search_queue:
        person = search_queue.popleft()
        if person not in searched:
            if person == target:
                return True
            else:
                search_queue += graph[person]
                searched[person] = True
    return False
```

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

Searching the graph for the target node is $O(E)$, where $E$ is the number of edges in the graph. Adding all neighbors to the queue is $O(V)$, where $V$ is the number of vertices in the graph. The total complexity of the algorithm is $O(V + E)$. This is a different way to express the linear time complexity $O(n)$ in the context of graphs.
