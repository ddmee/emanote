# Efficient Programs

Notes from [MIT Opencourseware CS 6-00sc sprint 2011](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00sc-introduction-to-computer-science-and-programming-spring-2011/unit-1/lecture-8-efficiency-and-order-of-growth/) by Prof John Guttag.

Getting your program quick enough to be useful

Why do some programs take much longer to run that others? It's possible, especially for certain problems, to write programs that could take a very long time to run.

Some computational programs are enormous. As the scale of problems grow, you have to be more careful about efficiency.

Efficiency is rarely about clever coding - choosing a clever instruction here or there. It's really about choosing the right algorthim.

Computer Scientists rarely invent new algorithms. Instead, we normally want to reduce the problem to a previously solved problem. We look at the problem and see how we can transform it into a solution someone else has already come up with.

## How do we think about effiency?

There's two important dimensions: space and time.

We can often trade one for the other.

## Time Complexity and Big O

See [[2022-03-06_1030_computational_complexity]]

## Growth rates

See [[2022-03-06_1040_graphs_of_growth]]

## Recursive factorial

See [[2022-03-06_1055_factorial]] which is O(n).

## Quadratic function

This next function seems to be a terrible way to compute `n*n` and it also runs in `O(n**2)` time. So it's quadratic.

```python
def g(n):
    x = 0
    for i in range(n):
        for j in range(n):
            x += 1
    return x
```

## Checksums

The next function adds together every decimal in a number. So it runs as many digits there are in the number. (Bit like a checksum.) The growth rate is basically `n/10`, as in everytime n grows by 10, the step increase by 1. Or `log10(n)` log based 10 n. It's the magnitude of the _length_ of (number of digits in) the integer X. See [[2022-03-06_1037_logarithms]] for background.

```python
def h(x):
    assert type(x) == int and x >= 0
    answer = 0
    s = str(x)
    for c in s:
        answer += int(c)
    return answer
```

**You must state time complexity in terms of the inputs to the program** rather than other things like local variables.

## Linear search

[[2022-03-06_1045_linear-search]] which is `O(length(n))` where n is list to search.

## Binary search

[[2022-03-06_1050_binary-search]] which is `O(log2(length(n)))`

## See sorting next...

MIT course continues onto [[2022-03-08_1816_sorting-a-list]]

## Hashing

And then onto hasing [[2022-03-11_0906-hashing]]

## Optimisation Problems

See on [[2022-03-16_1635_optimisation-problems]]

#complexity
#growth
#algorithms
#asymptotic
#bigO
#orderN
#omicron
#donaldknuth
