---
id: hash-tables
aliases:
  - Hash tables
tags: []
---

# Hash tables

Hash tables are a data structure that allows for the storing of _key-value pairs_. The advantage of a hash table is that each value can be accesses in $O(1)$ time in the best case by using the key. Hash tables are perfect for storing data that needs to be accessed quickly, when provided with a prompt. For example "What is the price of a banana?". The hash map would use the key "banana" to access the value "49 cents", instantly. This is much faster than iterating blindly over an [[arrays|array]] or [[linked-lists|linked list]] to find the answer. Accessing the data in this key-based way is called a _lookup_.

## Hash function

A hash function is where you put in a key, and you get a number. This number is the index of the array where the value is stored. The hash function is what makes hash tables so fast. It allows you to instantly locate the value in the array, without having to iterate over the entire array.

Imagine you have the array `["1 euro", "99 cents", "49 cents", "2 euros"]`. For each index in this array, you have a hash function that takes in the name of the product and returns the index of this array, where the price is stored. If I put in the key `"banana"` into the correct hash function, it will return the index `2`, which contains my answer `"49 cents"`. This is basically how a hash table works, it utilizes the combination of these hash functions and the array to store and retrieve data instantly.

The hash function is quite literally a function in the programming sense. The implementation can get quite complex, but it might look something like this:

```python
def hash_function(key):
    # Some computation to convert 'key' into a unique hash code
    hash_code = complex_computation(key)
    # Modulus operation to fit the hash code into the table size
    index = hash_code % size_of_the_table
    return index
```

This `complex_computation` involves many operations that are not important to understand for the rudimentary definition of hash tables and hash functions, but just imagine that this `hash_code` is some code that is unique to this specific key. It's important that the hash function always returns the same index for the same key, otherwise you might not be able to find the item again after it's been stored.

## Collisions

Collisions are an important concept when it comes to the performance of hash tables. In the ideal scenario, the hash function of a hash table will always map different keys to different indexes. In reality, it's almost impossible to write a hash function that does this.

Suppose you have a hash table that maps to an array with 26 slots, one for each letter of the alphabet. Then you want to put the price of bananas in the hash. All good so far, you get assigned the second index. Then you want to put the price of apples in the hash. You get assigned the first index. After this, you want to put the price of avocados in the hash. You also get assigned the first index. It turns out that there is a collision here, since different keys that start with the same letter will map to the same index. In short, a collision is when two keys get assigned the same slot. This is a problem.

Collisions can not be avoided. This is because there is an infinite amount of keys, but there is a finite amount of memory addresses in an array. Since they can't be avoided, they must be efficiently dealt with. The simplest way to deal with a collision is to store the values in a [[linked-lists|linked list]] at the index with the collision. So in the example described before, index `0` would map to `[("apple", "99 cents"), ("avocado", "1 euro")]`. This is called _chaining_. Index `1` would still map to `"49 cents"`, since there is no collision there.

Searching for the correct element is a bit slower in a linked list, but it's fine as long as the chain of collisions is not too big. But if you work at a grocery store that only sells product that start with the letter A, then you have one long linked list at index `0`, and an empty array for the rest. This is not ideal, and there are various ways to handle this situation that are too complex to cover for now, but looking into [[hashing-algorithms|hashing algorithms]] like [[sha|SHA]] is a good start. The key takeaways about collisions are:

- The hash function is very important. It should map the keys evenly across the array.
- Collisions are inevitable, and should be handled efficiently. The hash function is important in preventing as many collisions as possible.

## Load factor

The load factor of a hash table is the ratio between the number of items in the hash table and the total number of slots: $$ \text{number of items in hash table} \over \text{total number of slots} $$

A load factor lower than 1 means that the hash table is not full. A load factor higher than 1 means that the hash table is full and that there is a 100% chance there will be collisions, since there are more items than slots. Once the load factor starts to grow, it would be a good idea to add more slots to the hash table. This is called _resizing_. A rule of thumb would be to double the amount of slots once the load factor reaches 0.7.

Resizing takes time and it's an expensive operation, so you don't want to resize too often. But averaged out, hash tables still take $O(1)$ even with resizing taken into account.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

In the [[big-o#average-case|average case]], hash tables take $O(1)$ for everything, including searching, inserting and deleting elements. This means that they will always take the same time, no matter how big the hash table is. In the worst case these operations will take $O(n)$, but this is very unlikely. The worst case means that the hash table consists only of collisions.
