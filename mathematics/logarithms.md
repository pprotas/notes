---
id: logarithms
aliases:
  - Logarithms
tags: []
---

# Logarithms

Logarithms are inverse of [[exponents]]. If $2^4=2\times2\times2\times2=16$,
then $\log_2{16} = 4$.

So if you raise a number $n$ to the power of $x$, you get $n^x=y$. This means
that $log_n{y} = x$.

> [!example] What is $x$ in $log_3{81} = x$?
>
> This statement can be written as;
>
> $3^x=81$
>
> So how many times do we need to multiply $3$ by itself to get $81$?
>
> $3\times3\times3\times3=81$
>
> Therefore, $x=4$.

Logarithms have a special case if the input of the logarithmic function is $1$.
In this case, the output will always be 0.

> [!example] What is $x$ in $og_3{1} = x$?
>
> This statement can be written as;
>
> $3^x=1$
>
> This statement can ony ever be true if $x=0$.

## Logarithms and exponents

Logarithms are just another way of thinking about exponents. The difference is
that **the exponential form isolates the power**, while **the logarithmic form
isolates the exponent**.

| Logarithmic form | Exponential form |
| ---------------- | ---------------- |
| $log_2{8}=3$     | $2^3=8$          |
| $log_3{81}=4$    | $3^4=81$         |
| $log_5{25}=2$    | $5^2=25$         |

Choosing which form to use depends on the context of the mathematical problem.

## Definition of a logarithm

Generalizing the exmaples above leads us to the formal definition of a
logarithm.

$$ log_b(a) = c \iff b^c = a $$

Both equations describe the same relationship between $a$, $b$, and $c$:

- $b$ is the _base_
- $c$ is the _exponent_
- $a$ is the _argument_

> [!tip]
>
> The base of the logarithm is the same as the base of the exponent. Remember
> this when converting equations from the logartihmic form to exponential form,
> and the other way around.

The following restrictions apply to the variables:The following restrictions
apply to the variables: The following restrictions apply to the variables: The
following restrictions apply to the variables: The following restrictions apply
to the variables: The following restrictions apply to the variables:

| Restriction | Reasoning                                                                                                                                 |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| $b > 0$     | the base $b$ must always be positive.                                                                                                     |
| $a > 0$     | $log_b{a}=c$ means that $b^c = a$. Because a positive number raised to any power is positive, meaning $b^c > 0$, it follows that $a > 0$. |
| $b\neq{1}$  | $1$ to any power will always equal $1$.                                                                                                   |
