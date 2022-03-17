# Knapsack Problem

This is a classic example of an [[2022-03-16_1635_optimisation-problems|optimisation problem]]. It's [[an NP Hard problem|2022-03-06_1434_np_hard]]. In that a perfect solution requires expontential time. `O(2**n)` where n is the number of items. See [[2022-03-16_1814_absolute-optimal-knapsack-solution]].

Note, a knapsack is a backpack.

Problem: imagine you've limited space and want to maximise the amount of valuable items you put into that space. E.g. a burglar or a space rocket etc.

In terms of optimisation problem:

1. objective function = maximise value in the knapsack
2. a set of constraints = given how much the knapsack can carry.

Note, this is called a 0/1 knapsack problem. We can only take an entire item, not half of it or some other continuous amount. There is a version of the problem that deals with continous rather than discrete items.

## Absolute optimal solution

See [[2022-03-16_1814_absolute-optimal-knapsack-solution]]

## Greedy algorithm solution

See [[2022-03-16_1709_greedy-knapsack-algorithm]]

Note, for a continous version of this problem, a greedy algorithm provides an optium solution. But not for discrete (i.e. 1/0 knapsack) problems.

The problem with greedy alogorithms is that *local optimums at each step and combining them are not guaranteed to find the global optimum*.

The advantage of greedy algorithms is they are fast, relatively easy to code, and often produce a good guess.

## How good are these answers?


Also see [Knapsack Pattern Note](https://github.com/ddmee/Grokking-the-Coding-Interview-Patterns/blob/main/✅%20Pattern%2015:%200-1%20Knapsack%20(Dynamic%20Programming).md)

#algorithms
#optimisation
#complexity
#npcomplete
