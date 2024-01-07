---
id: arrays
aliases:
  - Arrays
tags: []
---

# Arrays

Sometimes you need to store a list of related elements in [[memory]]. Using an
array means that all your elements are stored contiguously (right next to each
other) in memory.

Arrays have a fixed size, even if not all of the slots of the array contain any
data in memory. This also means that if you want to resize an array to make it
bigger or smaller, you'll actually have to create a new array, and copy over the
old elements. This is by design, as it makes accessing the elements of the array
easy. You know the address of each element of the array, allowing fast _random
access_, where you can randomly access any of the elements without having to
traverse the others.

<!-- deno-fmt-ignore-start -->
The fact that the array elements are stored contiguously is also a big
advantage. This allows you to instantly locate the address of any of the
elements in the array, as long as you know the address of any of the elements
(and that element's index). This is not the case with [[linked-lists|linked lists]],
since you'd have to traverse the entire list to find the element you're looking
for.
<!-- deno-fmt-ignore-end -->

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

Reading an element from an array is $O(1)$, because you can instantly locate an
element by its index. Assigning a value to one of the array's addresses is also
$O(1)$, because you can instantly locate that address and simply assign the
value.

Adding an element to the start or middle of the array is different. This would
require shifting over the rest of the elements. Sometimes this would also mean
that a new array would have to be created, if there is not enough space. This is
an $O(n)$ operation, because you have to iterate over all the elements in the
array in the worst case. The same goes for deletions.
