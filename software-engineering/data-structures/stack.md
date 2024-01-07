---
id: stack
aliases:
  - Stack
tags: []
---

# Stack

A stack, when referring to the data structure, is a collection of elements that
you can interact with in a specific order. While the elements of [[arrays]] can
be accessed randomly, the elements of a stack can not. Instead, you can _push_
elements to the top of the stack, and you can _pop_ elements from the top of the
stack.

When pushing an element onto the stack, it is always added to the top. You can
not add an element to the middle or bottom of the stack. When popping an element
form the stack, you access the topmost element (the one that has most recently
been pushed), read its value, and then remove it from the stack. This means that
popping involves a read and a delete operation.

A good analogy for a stack is a stack of plates. When you stack plates in your
pantry, you will probably stack them on top of each other in the order you take
them out of the dishwasher. When you need a plate for your dish, you will take
the plate at the top, instead of a plate from the middle.
