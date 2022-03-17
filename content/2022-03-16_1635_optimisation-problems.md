# Optimisation Problems

How do we write programs that find optimal solutions to problems that occur in real life?

We can state optimisation problems as:

1. An objective function that will either be maximised or minimised.
2. A set of constraints that have to be satisfied.

Maximisation/minimisation of a function, e.g. finding the minimum price of a ticket between two destinations. Subject to the constraint that the journey won't take longer than X hours.

There are a lot of classic optimisation problems. And normally, when we come across a new problem we do problem reduction. Problem reduction - take a problem and map it onto an existing problem we know how to solve.

When we consider optimisation problems, we normally care about how well or how quickly we can solve the problem. However, the thing about optimisation problems is, unlike binary search algorithms etc, the nature of the problem normally means *there is no computational efficient algorithm to solve them*. They are typically much worse than the normal orders of growth, even worse than polynominal (See [[2022-03-06_1040_graphs_of_growth]]). In fact they can end up as [[2022-03-06_1434_np_hard]].

Instead we end up aiming for **approximate solutions** or best-effort solutions.

## Knapsack problem

One of the classic optimisation problems is the [[2022-03-16_1646_knapsack-problem]].

[[2022-03-16_1814_absolute-optimal-knapsack-solution]]

## Greedy algorithms

[[2022-03-16_1704_greedy-algorithm]]

[[2022-03-16_1709_greedy-knapsack-algorithm]]

## Inherently exponential for the worst case

Note, optimisiation problems often are *inherently exponential* to produce an algorithm that guarantees that the optimal/best solution is found. This is the runtime for the *worst case*. But, there are algorithms used to solve these problems fast enough to be useful.

## Machine Learning

Machine learning problems can often be seen as optimisation problems. See [[2022-03-17_0840_machine-learning]]

For unsupervised learning, we're often interested in clustering the data to classify it. Clustering can be tackled as an optimisation problem. See [[2022-03-17_1012_clustering]].


Notes from [MIT Opencourseware CS 6-00sc sprint 2011](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00sc-introduction-to-computer-science-and-programming-spring-2011/unit-2/lecture-18-optimization-problems-and-algorithms/) by Prof John Guttag.

#algorithms
#optimisation
#complexity
#clustering
