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

In the [[big-o#Worst case|worst case]] case, quicksort is $O(n^2)$, which is pretty slow, just as slow as the selection sort. In the [[big-o#Average case|average case]] case (which often resembles the best case), however, it is $O(n \log{n})$, which is much faster.

### Worst case

In the worst case, you will have to "touch" every element in the array, and then you have to recursively call the quicksort function on the remaining elements. So, for every element $n$, you have to perform $n-1, n-2\ldots 2, 1 \implies \frac{1}{2}\times n \implies n$ operations, since we [[big-o#Constants in Big O notation|ignore the constants]]. This is $O(n) \times O(n) = O(n^2)$.

This worst case is achieved when the pivot is consistently chosen poorly, such as when the pivot is the smallest or biggest number in the array. This leads to highly unbalanced partitions, and this in turn leads to more recursive calls.

### Best case

In the best case, you are able to split the array into two nearly equal parts by choosing a pivot that is in the middle of the array. If you are able to do this, then you've effectively halved the amount of recursive calls you still have to do until you hit the base case, which is an array with 1 element.

By consistently choosing a median pivot, the array is divided into approximately two equal halves at each recursive step, halving the number of remaining recursive calls. This division process, halving the array size each time, directly corresponds to the logarithmic term $log_2\,{n}$ in the complexity. The logarithm base 2 indicates the number of times the array can be halved before it is reduced to a single element (our base case).

You still have to "touch" every element in the array though, you just don't have to do it as many times because the base case is hit sooner. This is why the running time for quicksort in the best case is $O(n \log\,{n})$.

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

Turns out, if you pick a random pivot every time, quicksort will complete in $O(n \log{n})$ on average. This means that the average case is often also the best case. Here is how we can modify the code to pick a random pivot:

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

## Choosing a pivot

In the example, we chose a random pivot. This works, because on average the chosen pivot will be good enough, and choosing a random number is easy. This is not the only approach to choosing a pivot though.

| Strategy                                                                   | Pros                                                                 | Cons                                                                                                           |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Random element                                                             | Easy to implement, little overhead, good average-case performance    | Worst case is still possible                                                                                   |
| Median element                                                             | Always balanced partitions, consistent performance                   | Computational overhead of finding the median which can negate the performance gains, implementation complexity |
| Median-of-three (choose the median of the first, middle and last elements) | Balanced partitions, reduced worst-case chance, simple and efficient | Compromise, not always optimal                                                                                 |

Choosing a strategy can be a trade-off between performance, complexity and the chance of the worst case. You could get creative and fall back to random selection in some recursive steps if the median strategies are too expensive.
