---
id: call-stack
aliases:
  - Call stack
tags: []
---

# Call stack

The call stack, commonly referred to as simply the _stack_, is an important
concept in programming. The word "stack" is also used to refer to the
[[stack|data structure of the same name]], and indeed, the call stack is also
simply a stack that is used for a specific purpose within the runtime of a
programming language.

Most (not all) programming languages implement their own version of the call
stack. The way these various call stacks are implemented depends on the nuances
of the specific programming language. For example, the JavaScript call stack
runs within the JavaScript engine (like V8 or Node.js), while the Python call
stack is actually the call stack from C, which runs in the Python interpreter.

## Purpose

While the implementation of the call stack depends on the programming language,
they all serve the same purpose. When a program is running, it will call
different functions. These functions might call other functions, and then once
those functions are done, the origin function will continue. Other functions
might get called, and so forth.

Every time that a function is called, it will be pushed to the call stack.
Whatever logic is in this function will be executed, and if other functions are
called, then they are also pushed onto the call stack. At a certain point, the
function will be done, and it will be popped off of the call stack, so that the
program can move on. The call stack is constantly being pushed to and popped off
while running the program, until the program finishes.

## Example

Here you can see the call stack in action within a simple [[python|Python]]
program. The program consists of functions that print something, and also call
other functions. The operations of the call stack are numbered in the order they
are executed.

```python
def first_function():
    print("First")  # 1. print "First"
    second_function()  # 2. add second_function to the call stack
    fourth_function()  # 8. add fourth_function to the call stack
    # 11. pop first_function off the call stack


def second_function():
    print("Second")  # 3. print "Second"
    third_function()  # 4. add third_function to the call stack
    # 7. pop second_function off the call stack


def third_function():
    print("Third")  # 5. print "Third"
    # 6. pop third_function off the call stack


def fourth_function():
    print("Fourth")  # 9. print "Fourth"
    # 10. pop fourth_function off the call stack
```

Note that sub-functions are added to the call stack, even though the previous
function is not completed yet. At a certain point in this program, there are
three different functions in the call stack (until point #6, where the third
function is popped off).

The call stack also keeps track of the variables of each function:

```python
def my_function():
    my_variable = "hello"
    other_function("bye")
    print(my_variable)


def other_function(input):
    other_variable = input + " world"
    print(other_variable)
```

In the call stack above, you can imagine that the variables `my_variable`,
`input` and `other_variable` are kept in the call stack, along with their
corresponding methods.

## Stack overflow

Memory is not infinite, and so the call stack is not infinite either. Once too
many functions get piled on to the call stack without any pops, the call stack
will contain too many items, and the program will fail. This could be something
like a crash or a runtime error, depending on the programming language. Whenever
this happens, it's referred to as a _stack overflow_.

## Call stacks and recursion

[[recursion|Recursion]] works by calling itself over and over again. Each time
that a function calls itself, it is added again to the call stack. Only after
the base case is reached, will the functions start to pop off the stack, one by
one, until the first function call is reached again. In a way, we are zipping up
the call stack, until we reach the base case, and then we unzip all the way to
the bottom again. Satisfying!

<!-- deno-fmt-ignore-start -->
Note that if the base case is not reached within a certain number of recursive
calls, the stack will fill up too much, resulting in a [[#Stack overflow|stack overflow]].
<!-- deno-fmt-ignore-end -->

> [!tip]
>
> Rewriting a recursive function into an iterative function can often fix the
> stack overflow problem. This is because the iterative function would not have
> to keep track of the recursive calls in the call stack, instead it would use a
> loop to keep track over the iterations.
