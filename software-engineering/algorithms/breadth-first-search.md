---
id: breadth-first-search
aliases:
  - Breadth-first search
tags: []
---

# Breadth-first search

Breadth-first search is a search [[algorithms|algorithm]] that runs on [[graphs]]. It can answer whether there is a path between two distinct nodes, and what is the shortest path between them. The name of the algorithm comes from the fact that the algorithm searches the graph layer by layer, starting at the root node.

The core of the algorithm is that you start at the root node, and visit all of its neighbors. If none of the neighbors are the node you're searching for, you visit the neighbors of the neighbors. This continues until you find the desired node, or you run out of nodes to visit. Because of the breadth-first approach, the shortest path is also the very first path that is found, since the algorithm starts at the root node and works its way outwards

You can imagine looking for a specific person in your social network. You start with all of your 1st degree connections, and if that person is not found, you continue on to the 2nd degree connections - the friends of your friends. You continue on until you find the person you're looking for. The degree at which you find this person is the lowest possible degree, and thus the shortest path.

This approach of searching layer by layer is very fitting for [[queues]]. This is because each layer needs to be handled in the order that it was discovered.
