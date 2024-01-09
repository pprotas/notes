---
id: divide-and-conquer
aliases:
  - Divide and conquer
tags: []
---

# Divide and conquer

Divide and conquer (_D&C_) is a strategy for solving problems
[[recursion|recursively]]. It's not an [[algorithms|algorithm]], but an approach
to solving algorithms. D&C works by breaking the problem down into simpler steps
that are easier to solve.

D&C works like this:

1. Figure out a simple case as the base case
2. Figure out how to reduce your problem and get to the base case

For example, when recursively summing an [[arrays|array]] of numbers, you would
first figure out how to sum an array with just one number. This is step 1, the
base case. Then, you would figure out how to approach an array with multiple
numbers, while at the same time attempting to approach this base case you've
just set. This is step 2.

## Example

Let's apply D&C to this problem of summing an array of numbers recursively. The
simplest array to sum up are either empty arrays, or arrays with just one
number. This is our base case.

```python
def sum(arr):
  if len(arr) == 0:
    return 0
  elif len(arr) == 1:
    return arr[0]
```

Great, this is step 1 of D&C. The next step is to figure out how to divide the
problem until it becomes the base case. In the case of summing an array, we can
make the problem simpler by removing one number from the array, and then summing
the rest of the array until we hit the base case:

```python
def sum(arr):
  if len(arr) == 0:
    return 0
  elif len(arr) == 1:
    return arr[0]
 
  return arr[0] + sum(arr[1:])
```
