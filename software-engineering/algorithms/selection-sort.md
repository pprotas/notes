---
id: selection-sort
aliases:
  - Selection sort
tags: []
---

# Selection sort

A simple algorithm that sorts numbers from highest to lowest would involve
iterating through a list, and finding the highest number. Put this highest
number at the top, and repeat until you've exhausted the entire list. This is
called _selection sort_.

Selection sort works, but it's not very fast. [[quicksort]] is a faster sorting
algorithm.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

This is a $O(n)$ operation (you iterate through the entire list in the worst
case) that has to be repeated $n$ times (you need to repeat this for every
element in the list), therefore it is $O(n\times n)$, or $O(n^2)$ time.

## Example implementation

Here is an implementation of selection sort in [[python|Python]]. This function
sorts an array of numbers from lowest to highest.

```python
# utility function to find the index of the smallest number in the array
def find_smallest_index(array):
    smallest = array[0]  # start at the first element
    smallest_index = 0
    for i in range(
        1, len(array)
    ):  # iterate over each element until you find the smallest one
        if array[i] < smallest:
            smallest = array[i]
            smallest_index = i
    return smallest_index


def selection_sort(array):
    array_copy = array.copy()  # copy the array to prevent mutating the input
    new_array = []
    for _ in range(len(array_copy)):
        smallest_index = find_smallest_index(array_copy)
        new_array.append(
            array_copy.pop(smallest_index)
        )  # we remove the smallest element from the input list, and then add it to the start of new array
        # rinse and repeat
    return new_array
```
