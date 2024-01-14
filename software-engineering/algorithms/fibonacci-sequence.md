---
id: fibonacci-sequence
aliases:
  - Fibonacci sequence
tags: []
---

# Fibonacci sequence

The Fibonacci sequence describes a sequence of numbers where each number is the sum of the two preceding numbers. Calculating the $n\text{th}$ number in the sequence is a classic example of a problem that can be solved by a [[recursion|recursive]] algorithm. Not only is it a good example of recursion, it is also a good example of [[memoization]] and [[dynamic-programming|dynamic programming]], depending on the approach taken.

To calculate the sum of the preceding numbers, you need to calculate all Fibonacci numbers from $0$ to $n-1$. This makes calculating Fibonacci numbers a good example of a problem that has [[overlapping-subproblems|overlapping subproblems]].

## Recursive solution

The recursive solution for calculating Fibonacci numbers is very simple. It involves a base case and a recursive approach to solving the overlapping subproblems. Here is the recursive solution in [[python|Python]]:

```python
def fibonacci(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1

    return fibonacci(n - 1) + fibonacci(n - 2)
```

This approach works, but it's not very optimized. If you attempt to run this $n = 999$, it will take a long time. An even larger $n$ will result in a [[call-stack#Stack overflow|stack overflow]]

### Top-down approach - Recursive solution with memoization

Since the problem contains overlapping subproblems, it is a good candidate for memoization. Memoization is a form of caching that is specifically applied to functions and their results with specific arguments. In the case of the Fibonacci sequence, you can cache the results of the subproblems as long as you calculate them once. The next time you need to calculate the same subproblem, you can just use the cached result instead of recalculating it. This is called the top-down approach because you start with the big problem and break it down into smaller subproblems, and then you re-use the solutions to the subproblems to solve the big problem.

Here is a basic algorithm for calculating Fibonacci numbers using memoization in Python:

```python
def fibonacci(n):
    fibonacci_numbers = {0: 0, 1: 1}  # memoize every Fibonacci number in a map

    def ext(n):
        # only calculate the Fibonacci number if it's not memoized yet
        if n not in fibonacci_numbers:
            fibonacci_numbers[n] = ext(n - 1) + ext(n - 2)
        # after we memoize it, we can just get the number from the map
        return fibonacci_numbers[n]

    return ext(n)
```

This approach is already much faster than the regular recursive solution. The solution for $n = 999$ is calculated almost instantly. However, this approach is still recursive, and a larger $n$ will still result in a stack overflow.

There is a small optimization that can be made when it comes to the space complexity of this implementation. In the current implementation, every Fibonacci number is memoized. This is not necessary, since only the previous two numbers ($n - 1$ and $n - 2$) are needed to calculate the $n\text{th}$ number. Here is how that would look like:

```python
def fibonacci(n):
    def ext(n, a=0, b=1):  # use tail recursion with arguments a and b to memoize n - 2 (a) and n - 1 (b)
        # if n == 0 that means that a holds 0 and b holds 1
        if n == 0:
            return a

        # recursive call to n decremented by 1
        # a becomes n - 2, and b becomes the sum so far
        return ext(n - 1, b, a + b)

    return ext(n)
```

This approach uses less memory than the previous solution, but still suffers from stack overflows.

## Bottom-up approach - Iterative solution with tabulation

The iterative solution that uses dynamic programming converts the recursive calls from the previous memoized solution into a loop. It also starts at the bottom of the problem, where you calculate the Fibonacci numbers with the smallest index first, instead of starting at $n$ and decrementing it by 1 each time. This is characteristic of a _bottom-up_ approach. Here is how that would look like:

```python
def fibonacci(n):
    if n == 0:  # no need to calculate anything if n == 0
        return 0

    # tabulate all Fibonacci numbers in an array
    fibonacci_numbers = [0, 1]

    # we start at n = 2 (because we know n_0 = 0 and n_1 = 1), and calculate every Fibonacci number up till n
    for i in range(2, n + 1):
        a = fibonacci_numbers[i - 2]
        b = fibonacci_numbers[i - 1]

        fibonacci_numbers.append(a + b)

    return fibonacci_numbers[n]
```

There is no recursion used here at all. It's just a loop that goes from $2\cdots n-1$ and calculates each Fibonacci number on the way, and then _tabulating_ (caching) them in an array. At the end, the value at index $n$ in the array holds the Fibonacci number for $n$.

Not only is this implementation more efficient, it also does not suffer from stack overflow. You can calculate the Fibonacci number for very large $n$, almost instantly.

### Optimizing for space

As the cherry on top, there is a small implementation that can be made to the algorithm that will result in less memory usage. Instead of tabulating every Fibonacci number along the way, one can simply cache the last two computations. This is possible because the Fibonacci number for $n$ is the sum of the Fibonacci numbers for $n - 1$ and $n - 2$. Here is how that would look like:

```python
def fibonacci(n):
    if n == 0:  # no need to calculate anything if n == 0
        return 0

    # cache only the last two computations
    a = 0  # n - 2
    b = 1  # n - 1

    # we start at n = 2 (because we know n_0 = 0 and n_1 = 1), and calculate every Fibonacci number up till n
    for _ in range(2, n + 1):
        # calculate the next n - 1 and then move it up in the cache
        current = a + b
        (a, b) = (b, current)

    # the Fibonacci number for n is the last computation, which is b
    return b
```

There is no recursion used here at all. It's just a loop that goes from $2\cdots n-1$ and calculates each Fibonacci number on the way, and then caching them in `a` and `b`. At the end, the value `b` holds $F(n - 1) + F(n - 2)$, which is the Fibonacci number for $n$.
