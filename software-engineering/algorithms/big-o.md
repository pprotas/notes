---
id: big-o
aliases:
  - Big O
tags: []
---

# Big O

Big O notation is special notation that tells you how fast an algorithm is. It
tells you this, by giving you an idea of how the running time of the algorithm
increases as the size of the input increases.

## Notation

The Big O notation is written by a "big O" $O$, followed by the number of
operations, often expressed in $n$.

> [!example]
>
> The [[binary-search|binary search]] algorithm has a running time of
> $O(log_2{n})$, while the simple search algorithm has a running time of $O(n)$.
> This means that, even though simple search might be "fast enough" for small
> lists, it will be much, much slower than the binary search algorithm for
> larger lists.
>
> You can imagine a graph for the running time of both algorithms. The simple
> search is a linear graph that will increase in a straight line for every
> element added to the list. The binary search is a logarithmic graph that will
> eventually flatten out towards its asymptote.

## Worst case

Big O notation establishes a worst-case run time. An algorithm might find the
input you're looking for within 1 operation. That's great, but what if you input
a million inputs? In this worst-case, the algorithm might take a million
attempts. Just because you found the input using simple search on the first try,
doesn't mean that it's running time is $O(1)$, because in the worst case it
would have been $O(n)$.

## Common Big O run times

| Big O               | Example                                                 |
| ------------------- | ------------------------------------------------------- |
| $O(log(n))$         | Binary search (fast)                                    |
| $O(n)$              | Simple search (slow)                                    |
| $O(n\times log(n))$ | [[quicksort\|Quicksort]] (fast)                         |
| $O(n^2)$            | [[selection-sort\|Selection sort]] (slow)               |
| $O(n!)$             | [[traveling-salesperson\|Traveling salesperson]] (slow) |

## Constants in Big O notation

Constants in Big O notation are often ignored. For example, during
[[selection-sort|selection sort]], the amount of list items that you'll have to
traverse decreases over time, as the list progressively becomes more sorted. At
first you'll have to traverse $n$ items, then $n - 1, n - 2, n - 3 \ldots 2, 1$.
On average, you'll have to check a list that has $\frac{1}{2}\times n$ elements.
The runtime would then be $O(n\times\frac{1}{2}\times n)$. But constants like
$\frac{1}{2}$ are ignored, so the runtime is simply $O(n^2)$.
