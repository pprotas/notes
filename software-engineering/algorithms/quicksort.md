---
id: quicksort
aliases:
  - Quicksort
  - quicksort
  - quicksort\
tags: []
---

# Quicksort

Quicksort is a sorting [[algorithms|algorithm]] that is much faster than [[selection-sort|selection sort]]. Quicksort uses the [[divide-and-conquer]] approach, which means that it has a base case and a [[recursion|recursive]] case.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

In the [[big-o#Worst case|worst case]] case, quicksort is $O(n^2)$, which is pretty slow, just as slow as the selection sort. In the [[big-o#Average case|average case]] case, however, it is $O(n \log{n})$, which is much faster. The complexity of quicksort is best explained with an explanation, so read ahead!

<!-- TODO: The complexity is explained with an explanation, but there's probably a way to explain it in a more general way, and make the heading about example implementation shorter -->

## Example implementation

Let's implement quicksort in [[python|Python]].

Quicksort's base case is that arrays that are empty or have just one element do not need to be sorted, since there is no way to sort them:

```python
def quicksort(arr):
    if len(arr) < 2:
        return arr
```

For arrays with the size of 2, you can check which number is bigger and return them in a sorted order:

```python
def quicksort(arr):
    if len(arr) < 2:
        return arr
    elif len(arr) == 2:
        first = arr[0]
        second = arr[1]
        return [first, second] if first < second else [second, first]
```

For arrays bigger than that, you need to approach the problem a bit differently. You need to pick a _pivot_, which is a specific element in the array. Then, divide the rest of the array into two parts: 1. every number smaller than or equal to the pivot and 2. every number bigger than the pivot. This is called _partitioning_.

Afterwards, you can recursively call the quicksort function on both partitions and concatenate them with the pivot in the middle:

```python
def quicksort(arr):
    if len(arr) < 2:
        return arr
    elif len(arr) == 2:
        first = arr[0]
        second = arr[1]
        return [first, second] if first < second else [second, first]

    pivot = arr[0]
    lhs = [x for x in arr[1:] if x <= pivot]
    rhs = [x for x in arr[1:] if x > pivot]
    return quicksort(lhs) + [pivot] + quicksort(rhs)
```

Turns out, you don't need to explicitly check the base case when the array is 2 elements big. This is because the partitioning approach will also work for this size of array:

```python
def quicksort(arr):
    if len(arr) < 2:
        return arr

    pivot = arr[0]
    lhs = [x for x in arr[1:] if x <= pivot]
    rhs = [x for x in arr[1:] if x > pivot]
    return quicksort(lhs) + [pivot] + quicksort(rhs)
```

Notice how we applied D&C here. We figured out the simplest case, which is arrays with less than 2 elements. Then, we figured out how to reduce the problem to the base case, which is partitioning the array.

The algorithm works because of this base case. You can just keep calling `quicksort` on the partitions until you hit the case where the array has less than 2 elements. After that, the sorted arrays will propagate back up the recursive chain, until the first call to `quicksort` returns the fully sorted array.

We are not done yet. This implementation of quicksort is not optimal, since the pivot element is always the first element of the input array. With this approach, there is more chance that the algorithm will run in its worst case, so it will run much slower than we'd like. This is because the worst case of quicksort is that the input array is already sorted. Imagine that the input array is `[1, 2, 3, 4, 5, 6, 7, 8]`. With our current implementation, you will keep having an empty `lhs`, the pivot will be the first element, and `rhs` will just be everything else. The height of the [[call-stack|call stack]] in this scenario will be 8, since every number but the last will have a turn to be the pivot.

The best case for this same sorted input array is that the pivot is always the middle element. This way, each partition will be half the size of the input array minus the pivot, and the height of the call stack will be reduced to 4.

In the worst case, there are $O(n)$ levels in the call stack (each element is a pivot), and each level takes $O(n)$ to complete (you have to touch every element to subdivide them into partitions). This is $O(n) \times O(n) = O(n^2)$ time.

In the best case, there are still $O(n)$ levels, but each level takes $O(\log{n})$ to complete because the array is divided in half every time. This results in $O(n) \times O(\log{n}) = O(n \log{n})$ time.

Turns out, if you pick a random pivot every time, quicksort will complete in $O(n \log{n})$ on average. This means that the average case is also the best case. Here is how we can modify the code to pick a random pivot:

```python
import random

def quicksort(arr):
    if len(arr) < 2:
        return arr

    pivot = random.choice(arr)
    lhs = [x for x in arr[1:] if x <= pivot]
    rhs = [x for x in arr[1:] if x > pivot]
    return quicksort(lhs) + [pivot] + quicksort(rhs)
```
