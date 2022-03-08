# Computational Time Complexity. Issues around time.

## Question: how long does a program take to run? How would we answer that?

We could run it on a computer and time it. Then we could compare the results. That's a bad way to think about it. For a start, it's not a stable measure. The speed of the machine matters. The cleverness of the programming language implementation will also impact it. Plus, we won't know until we run it how long it should take. What if the program never completes? What if the program is meant to complete but doesn't seem to? It also depends on the input. What happens if I give the program a big input? That'll take longer than giving it a smaller input.

So this approach has too many variables to control.

Instead, **what we do is count the number of basic steps in the program**.

Define a function: `T: N -> N`

Time: Size of the input -> Number of Steps computational will take

A step is a computation that takes a constant time. So steps are not variable. They are a constant operations. E.g. an assignment, a variable access, addition etc.

## RAM model

We are going to use a model of computation called a Random Access Machine (RAM). See [[2022-03-06_1035_ram_model]]. This is to abstract away some of the complexities of hardware varieties towards something that is often roughly correct. Would be interesting to know ways we can break this model.

## Question: if we are considering the number of steps a program will take over it's inputs, which of these inputs are we interested in?

- Best case - the minimum running time over all possible inputs
- Worst case - the maximum running time over all possible inputs
- Average/expected case - the typical running time over all possible inputs

The average/expected case seems like the one we should care about. The Best case is too optimistic. The expected case is hard because we have to think about what the distribution of queries looks like. The expected case really depends on the frequency of particular inputs to the function. If we get a lot of 'best' cases as queries, then the expected case looks better. Whereas if we get a lot of pathological/worst-cases, then the average looks a lot slower. But a lot of the time, before we deploy an algorithm, we don't know what distribution of inputs it'll actually recieve.

Thus calculating the average running time is harder than calculating the worst case. In reality, we usually care about the worst case (murphy's law) when we compute complexity of a program.

## Lets look at an example

```python
def f(n):  # calculates factorial
    assert n >= 0
    answer = 1
    while n > 1:
        answer *= n
        n -= 1
    return answer
```

How many times through the loop? It goes n times. Everytime it goes through the loop, it does 3 steps. It also has a two steps at the start that are not repeated plus the return statement at the end. So the number of steps is: `n*3 + 2 + 1`.

But the constants are not really relevant. Say n is 3000. That's 9003 steps. Do I care whether it's 9000 or 9003?

We ignore additive constants like the inital step costs. To characterise the algorithm we can ignore those. What we really care about is **growth with respect to input growth**.

So that leaves us with `3n`.

We can go further. Do we really care if it's 3000 or 9000? Well I might. As it gets bigger and bigger, i.e. if it takes 3000 years verus 9000 years, does that really matter to us? It's too long anyway.

So typically we even ignore multiplicative constants. We use a model of **asymptotic growth** that talks about how complexity grows as we reach the limits of the sizes of the input.

We typically do this using notation called Big O notation.

We write: `O(n)`. That we call 'Order N'. That means running time grows linearly with the size of the input N. It's not actually a big O. It's the greek symbol Omicron. (Choosen by Donald Knuth) We typically use latin letter O because it's easier to type.

For example, we can write that a function with X input, computation time grows at x squared. The function f grows no faster than the quadratic polynomial x squared.

```
f(x) = O(x**2)
```

See [[2022-03-06_1040_graphs_of_growth]] for orders of growth.

#complexity
#growth
#algorithms
#asymptotic
#bigO
#orderN
#omicron
#donaldknuth
