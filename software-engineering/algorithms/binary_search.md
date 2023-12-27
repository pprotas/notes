---
id: binary_search
aliases:
  - Binary Search
tags:
  - algorithm
---

# Binary Search

Binary search is an [[algorithms|algorithm]] which returns the position of a
desired element from a sorted list.

A naive way to search for an element of the list would be by iterating through
every element until the desired element is found. This is called the _simple
search_ Imagine an array with integers from 1 to 100. If you're trying to guess
a specific number, you could start at 1 and guess every number until you find
the correct one. Every guess is reciprocated with the feedback of whether your
guess is too low, or correct. If the number is 99, it would take you 99 guesses
to get there.

Binary search approaches the same problem in a different way. Instead of
iterating through the elements one by one, the array is divided in half, and the
algorithm guesses the number in the middle (50). If the number is too low,
divide the first half and guess again (25). If it's too high, divide the second
half and guess again (75). Repeat until the correct number is found. Every guess
eliminates so many numbers, that it would only ever take 7 attempts to guess the
right integer in this array from 1 to 100.

## Complexity

> [!info] See [[big_o|Big O]] notation

In the worst case of $n$ elements, binary search will take $\log_2 n$ steps to
run. Simple search will take $n$ steps in the worst case.
