---
id: big-o
aliases:
  - Big O
tags: []
---

# Big O

Big O notation is special notation that tells you how fast an algorithm is. It tells you this, by giving you an idea of how the running time of the algorithm increases as the size of the input increases.

<!-- TODO: Space complexity, and how it differs from time complexity. -->
<!-- TODO: Update notes on algorithms with both space and time complexity. -->
<!-- TODO: Write about space-time trade off. -->

## Notation

The Big O notation is written by a "big O" $O$, followed by the number of operations, often expressed in $n$.

> [!example]
>
> The [[binary-search|binary search]] algorithm has a running time of $O(log_2{n})$, while the simple search algorithm has a running time of $O(n)$. This means that, even though simple search might be "fast enough" for small lists, it will be much, much slower than the binary search algorithm for larger lists.
>
> You can imagine a graph for the running time of both algorithms. The simple search is a linear graph that will increase in a straight line for every element added to the list. The binary search is a logarithmic graph that will eventually flatten out towards its asymptote.

## Worst case

Big O notation establishes a worst-case run time. An algorithm might find the input you're looking for within 1 operation. That's great, but what if you input a million inputs? In this worst-case, the algorithm might take a million attempts. Just because you found the input using simple search on the first try, doesn't mean that it's run time is $O(1)$, because in the worst case it would have been $O(n)$.

### Average case

The average case means that the algorithm will run in this time on average. So if you run the algorithm a bunch of times, on average it will come close to this run time. [[quicksort|Quicksort]] run in $O(n^2)$ in the worst case, but in $O(n \log{n})$ in the average case. So even though the worst case is pretty slow, on average it will be pretty fast.

## Common Big O run times

Here are some common run times, sorted by their efficiency, from fastest to slowest:

| Name               | Big O          | Example                                                 |
| ------------------ | -------------- | ------------------------------------------------------- |
| Constant           | $O(1)$         | Accessing an [[arrays\|array]] element by its index     |
| Logarithmic        | $O(log\,n)$    | Binary search (fast)                                    |
| Linear             | $O(n)$         | Simple search (slow)                                    |
| Linear logarithmic | $O(n\;log\,n)$ | [[quicksort\|Quicksort]] (fast)                         |
| Quadratic          | $O(n^2)$       | [[selection-sort\|Selection sort]] (slow)               |
| Factorial          | $O(n!)$        | [[traveling-salesperson\|Traveling salesperson]] (slow) |

## Constants in Big O notation

Constants in Big O notation are often ignored. For example, during selection sort, the amount of list items that you'll have to traverse decreases over time, as the list progressively becomes more sorted. At first you'll have to traverse $n$ items, then $n - 1, n - 2, n - 3 \ldots 2, 1$. On average, you'll have to check a list that has $\frac{1}{2}\times n$ elements. The runtime would then be $O(n\times\frac{1}{2}\times n)$. But constants like $\frac{1}{2}$ are ignored, so the runtime is simply $O(n^2)$.

### Time constants

When you use the Big O notation, you're not concerned with the exact measurement of time that the algorithm will take. You're talking about the complexity of the algorithm, not how many seconds it takes to run it. And yet, there is a small nuance related to this that can make a big difference in your choice of algorithm.

When you say $O(n)$, you're actually saying something like $c \times n$, where _constant_ $c$ is some fixed amount of time that the algorithm takes. You usually ignore that constant, because if two algorithms have different Big O times, the constant does not matter. Take binary search and simple search, for example. Suppose both algorithms had these constants:

| Simple Search   | Binary Search        |
| --------------- | -------------------- |
| $10ms \times n$ | $1sec \times log(n)$ |

Simple search has a constant of 10ms, which seems way faster than the 1s constant of binary search. And yet, if you do the math for an $n$ of 4 billion elements, simple search will take 463 days and binary search will take 32 seconds. The constant did not make a difference at all.

But sometimes the constant can make a difference. Quicksort versus [[merge-sort|merge sort]] is one example. Quicksort has a smaller constant than merge sort. Since they are both $O(n log{n})$, quicksort is faster due to its smaller constant in the average case.
