---
id: recursion
aliases:
  - Recursion
tags: []
---

# Recursion

Recursion is when a function calls itself in its own definition. This is a concept in programming, used when implementing various [[algorithms]]. While all algorithms that use recursion can also be implemented by using iterative loops, both approaches have their pros and cons.

Using loops can result in a performance boost, or they can result in more efficient use of resources like memory. On the other hand, code involving loops (especially nested loops) can be harder to read and understand. This is where recursion shines; as long as you understand the concept of recursion, code can be easier to read and understand. This can come at the cost of [[call-stack#Call stacks and recursion|memory problems]], or slower code. The programming language used, and the algorithm in question are important factors to consider when choosing between loops or recursion.

## Structure of a recursive function

Since recursive functions call themselves, they need a way to know when to stop executing, otherwise they will run forever, resulting in an infinite loop. That's why every function has two parts: a _base case_ and the _recursive case_. The recursive case is when the function calls itself. The base case is when the function doesn't call itself again, so that the infinite loop is prevented.

In a way, the base case is the "stop" condition of the function; the desired outcome has either been reached, or the function has reached its limit (for example, all of the elements of the input array have been traversed and nothing else can be done).

On the other hand, the recursive case is the "continue" condition of the function; during this specific iteration of the function, there is still something to do, so the function has to call itself again.

Here is an example of a recursive function:

```python
def countdown(i):
    print(i)
    if i == 0: # base case
        return
    else: # recursive case
        countdown(i - 1)
```

After printing a number, the function goes into checking the base or recursive case. In the base case, we have to check whether our desired outcome has been reached. In other words, is the countdown function done with counting down to 0? If this is indeed the case, we can stop the execution of the function. Without the base case, the function would keep counting down forever.

If this is not the case yet, we go into the recursive case. Apparently, the countdown is not done yet, and therefore we have to call the countdown function again, but now with a different input. In the case of the countdown function, we keep counting down, so our input is one less than the one we had before. Without the recursive case, the function would never call itself again with the next iteration of input(s), and therefore the recursion would stop.
