---
id: linked-lists
aliases:
  - Linked lists
tags: []
---

# Linked lists

A linked list is a collection of elements (_nodes_) in [[memory]]. These nodes
can be stored anywhere in memory. They don't have to be stored contiguously,
like [[arrays]]. This is because of their design, where each node stores the
address of the next node in the list. This way, a bunch of random memory
addresses are linked together.

Adding an node to a linked list is easy. You stick an node anywhere in memory,
and make sure that it properly references the previous and next nodes. You can
read any desired node by starting at the first node and following the references
to the next node until you reach the desired node. This is called _sequential
access_, where you _traverse_ through the nodes.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

Reading an node from a linked list is $O(n)$, because you have to traverse the
entire list, node by node, to get the node you're looking for. In the worst
case, you'd have to traverse the entire array.

On the other hand, inserting an node into a linked list can be $O(1)$, because
you can just stick it anywhere in memory and update the previous/next
references. This assumes that you already know this position, otherwise you'd
have to traverse the list first ($O(n)$) to get the reference to either the
previous or next node. The same goes for deletions.
