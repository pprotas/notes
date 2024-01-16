---
id: arrays
aliases:
  - Arrays
tags: []
---

# Arrays

Sometimes you need to store a list of related elements in [[memory]]. Using an array means that all your elements are stored contiguously (right next to each other) in memory.

Arrays have a fixed size, even if not all of the slots of the array contain any data in memory. This also means that if you want to resize an array to make it bigger or smaller, you'll actually have to create a new array, and copy over the old elements. This is by design, as it makes accessing the elements of the array easy. You know the address of each element of the array, allowing fast _random access_, where you can randomly access any of the elements without having to traverse the others.

The fact that the array elements are stored contiguously is also a big advantage. This allows you to instantly locate the address of any of the elements in the array, as long as you know the address of any of the elements (and that element's index). This is not the case with [[linked-lists|linked lists]], since you'd have to traverse the entire list to find the element you're looking for.

## Complexity

> [!info]
>
> See [[big-o|Big O]] notation

Reading an element from an array is $O(1)$, because you can instantly locate an element by its index. Assigning a value to one of the array's addresses is also $O(1)$, because you can instantly locate that address and simply assign the value.

Adding an element to the start or middle of the array is different. This would require shifting over the rest of the elements. Sometimes this would also mean that a new array would have to be created, if there is not enough space. This is an $O(n)$ operation, because you have to iterate over all the elements in the array in the worst case. The same goes for deletions.

## Details on the numbering of the array indices

Junior programming students will undoubtedly notice an interesting fact about accessing array elements at any index: the indices are offset by one from the actual index that we intuitively expect it to be. So the first element of the array is found at index `0`, the second one at index `1`, and the 1000th element is found at index `999`. Although this is not the case in every programming language (for example [[lua|Lua]], which starts indexing at `1`), it is the case for most modern programming languages.

The designers of these programming languages did not choose to start the indexing at 0 for arbitrary reasons. There is no technical limitation that keeps them from starting it at 1, either. The reason has a lot to do with math and [[natural-numbers|natural numbers]], and the fact that we include `0` as a natural number in computer science (as opposed to the field of mathematics, where natural numbers start at `1`). Suppose you were to denote a sequence of natural numbers in mathematical notation $2, 3, \dots, 12$ without the dots. There are four possible ways to do this:

$$ \text{a)}\; 2 \le i \lt 12 $$

$$ \text{b)}\; 2 \lt i \le 12 $$

$$ \text{c)}\; 2 \le i \le 12 $$

$$ \text{d)}\; 2 \lt i \lt 12 $$

What would be a good reason to prefer one over the other? Option $a$ and $b$ have the benefit that the difference between the lower and upper bound equals the length of the sequence between the bounds. This is a valid point, but it's not enough to decide on one or the other. The other benefit of $a$ and $b$ is that two adjacent sequences can be combined into one single sequence because the lower bound of one subsequence would be the upper bound of the other, like so:

$$ 2 \le i \lt 12 \le j \lt 22 $$

Another valid point, but still not enough to choose $a$ over $b$ or vice versa. So what would be a good reason?

There is a smallest natural number. Excluding the lower bound, just like in option $b$ or $d$, would mean that there is no clear way where the counting of a sequence should start. In the example, is the starting number $2.1$? Or is it $2.0001$? Or $2.0000001$? This is ugly. There is no clear way to start counting at a natural number if the lower bound is excluded. Therefore we need to include the lower bound like in option $a$ or $c$.

On to the upper bound. If the lower bound is included like we mentioned before, then the notation stops making sense if the upper bound is also included and the sequence shrinks to 0 (it is empty). It would look like $0\le i \le 0$, which doesn't make sense because it implies that it's possible that $i$ can take on the value of $0$, which is impossible because the sequence is empty. Remember: we said that the sequence is empty, so how is it possible that it contains the element $i = 0$? All of this logic implies that the upper bound should be excluded, like in option $a$ or $d$.

The only option that fits both criteria is $a$, so this notation is to be preferred. Alright, makes sense, but what does this have to do with starting the indexing at `0`? Well let's say that you have a sequence with length of $N$, and you want to access an element of the sequence using an index $i$. If the indexing starts at `1`, that means that $1 \le i \lt N + 1$ if we go with the notation in option $a$, the only logical notation. We want to get rid of that $+ 1$, it does not look nice. So, we start the indexing at `0`, resulting in $0 \le i \lt N$. This is the reason why most programming languages start indexing at `0`.

> [!note] Edsger W. Dijkstra
>
> We gave Edsger W. Dijkstra to thank for this explanation above, because most of this is paraphrased from his document [EWD831](https://www.cs.utexas.edu/users/EWD/ewd08xx/EWD831.PDF). He was a legendary Dutch computer scientist and programmer, who analyzed this problem and explained it in detail, although the convention was already in use before he wrote about it. He also invented [[dijkstras-algorithm|Dijkstra's algorithm]].

There is also a practical reason for this that has less to do with math, and more to do with how the arrays are stored in memory. The elements of the array are stored in memory as one contiguous block of memory, and the base address of the array points to the first element. You calculate the address of the $n$-th element of an array like so:

$$ \text{Address of the $n$-th element} = \text{Base address} + (n \times \text{Size of the element}) $$

If we start the indexing at `0`, this calculation is simpler because then the base address is equal to the address of the first element. The calculation of _offsets_ is also easier this way, since the element at index $4$ is also offset by 4, so it is "4 elements from the base address".
