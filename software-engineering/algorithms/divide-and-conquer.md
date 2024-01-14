---
id: divide-and-conquer
aliases:
  - Divide and conquer
tags: []
---

# Divide and conquer

Divide and conquer (_D&C_) is a strategy for solving problems [[recursion|recursively]]. It's not an [[algorithms|algorithm]], but an approach to solving algorithms. D&C works by breaking the problem down into simpler steps that are easier to solve.

D&C works like this:

1. Figure out a simple case as the base case
2. Figure out how to reduce your problem and get to the base case

For example, when recursively summing an [[arrays|array]] of numbers, you would first figure out how to sum an array with just one number. This is step 1, the base case. Then, you would figure out how to approach an array with multiple numbers, while at the same time attempting to approach this base case you've just set. This is step 2.

This main approach of determining the base case first, and then working your input toward that base case is the key characteristic of D&C algorithms. This type of approach lends itself well to recursive solutions. This is different from [[greedy-algorithms|greedy algorithms]], which don't care about the base case, and instead focus on the current step only. D&C algorithms like to reduce the current input to the base case, instead of making the locally optimal choice. They want to work towards a known end state.

An example of this would be [[quicksort]]. Quicksort has a base case in mind: there should only be two or less elements in the input array. But what if you have more than two elements? Well, then you need to find a way to reduce the amount of elements to 2 or less, somehow. This fits exactly into the definition of D&C, quicksort has a base case and is reducing the problem to get to the base case. Compare this to a greedy algorithm like [[dijkstras-algorithm|Dijkstra's]]. Dijkstra's algorithm doesn't care about any base case or known end state. It only cares about the current step, and which node is the fastest to get to at that point in time.

## Example

Let's apply D&C to this problem of summing an array of numbers recursively. The simplest array to sum up are either empty arrays, or arrays with just one number. This is our base case.

```python
def sum(arr):
  if len(arr) == 0:
    return 0
  elif len(arr) == 1:
    return arr[0]
```

Great, this is step 1 of D&C. The next step is to figure out how to divide the problem until it becomes the base case. In the case of summing an array, we can make the problem simpler by removing one number from the array, and then summing the rest of the array until we hit the base case:

```python
def sum(arr):
  if len(arr) == 0:
    return 0
  elif len(arr) == 1:
    return arr[0]
 
  return arr[0] + sum(arr[1:])
```
