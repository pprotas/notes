---
id: graphs
aliases:
  - Graphs
tags: []
---

# Graphs

A graph models a [[sets|set]] of connections. It represents a network of _nodes_, which are also called _vertices_. These vertices are connected to each other by _edges_, which represent the distance between the nodes. Nodes connected by an edge are called _neighbors_. Graphs are a way to model how different things are connected to another. Examples of graphs are networks of friends on social media, a map of roads between cities or the metro system of a city.

_Directed graphs_ represent a one-way relationship between the nodes where the edges go from one node to another in a specific direction, while _undirected graphs_ represent the fact that the edge is bi-directional.

## Trees

A tree is directed graph without any cycles. Think of a family tree, where a specific family member's parents are represented by directed edges towards their parents, and the edges of the parents link to the grandparents and so forth. The edges never point backward.

## Weighted graphs

A weighted graph is a graph where each edge has a numerical value associated with it. This value is called the _weight_. The weights represent some kind of numerical relation between the nodes. For example, a weight between two nodes could represent the distance in kilometers between two cities, or the amount of minutes between two bus stops.

## Example implementation

Graphs can be implemented in many different ways. A simple way to implement a directed graph is to use [[hash-tables|hash tables]], since hash tables contain a key (the node) and a value (the corresponding neighbors). Here is an example implementation in [[python|Python]]:

```python
graph = {}
graph["you"] = ["alice", "bob", "claire"]
graph["bob"] = ["anuj", "peggy"]
graph["alice"] = ["peggy"]
graph["claire"] = ["thom", "jonny"]
graph["anuj"] = []
graph["peggy"] = []
graph["thom"] = []
graph["jonny"] = []
```
