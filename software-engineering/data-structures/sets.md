---
id: sets
aliases:
  - Sets
tags: []
---

# Sets

Sets are collections of unordered, unique items. The _unique_ part is what makes sets unique. Every element in the set can only appear once, and an attempt to add an element that already exists in the set will have no effect. The idea for the set data structure comes from a mathematical concept of the same name.

Sets are unordered, which means that you cannot access elements by their index. This means that you cannot get the first element, the last element, or any element in between. This is why sets are not a good choice if you need to access elements by their index.

On the other hand, sets are very good at checking whether an element exists in the set or not. They are very efficient when it comes to inserting, deleting and reading from the set by value. This is because sets use [[hash-tables|hash tables]] under the hood, which are very efficient at these operations. The difference between a set and hash map is that sets only store keys, and don't store the associated values. Hash maps store keys and their associated value.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

Since sets are implemented using hash tables, they have the same complexity as hash tables. The complexity of sets in the average case is $O(1)$ for insertion, deletion and lookup. In the worst case, the complexity is $O(n)$ due to hash collisions. This would happen when the hash function for these elements is poorly designed.
