---
id: binary-search
aliases:
  - Binary Search
tags:
  - algorithm
---

# Binary Search

Binary search is an [[algorithms|algorithm]] which returns the position of a desired element from a sorted list.

A naive way to search for an element of the list would be by iterating through every element until the desired element is found. This is called the _simple search_ Imagine an array with integers from 1 to 100. If you're trying to guess a specific number, you could start at 1 and guess every number until you find the correct one. Every guess is reciprocated with the feedback of whether your guess is too low, or correct. If the number is 99, it would take you 99 guesses to get there.

Binary search approaches the same problem in a different way. Instead of iterating through the elements one by one, the array is divided in half, and the algorithm guesses the number in the middle (50). If the number is too low, divide the first half and guess again (25). If it's too high, divide the second half and guess again (75). Repeat until the correct number is found. Every guess eliminates so many numbers, that it would only ever take 7 attempts to guess the right integer in this array from 1 to 100.

> [!warning]
>
> Binary search only works on sorted lists. If the list is not sorted, there is no way to know in which "half" the next guess should take place.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

In the worst case of $n$ elements, binary search will take $\log_2 n$ steps to run - $O(log(2))$. Simple search will take $n$ steps in the worst case - $O(n)$.

## Example implementation

Here is an implementation of binary search in [[python|Python]]:

```python
def binary_search(list, item):
    # low and high are initially the first and last indexes of the list
    low = 0
    high = len(list) - 1

    while low <= high:  # while there are still elements to search
        # get the middle index
        # this Python syntax is called integer division, which rounds down
        mid = (low + high) // 2

        guess = list[mid]

        if guess == item:
            return mid
        # adjust high or low based on whether the guess was too high or too low
        # the next iteration will use the new high/low values, searching in the correct half of the list
        if guess > item:
            high = mid - 1
        else:
            low = mid + 1
    return None
```
