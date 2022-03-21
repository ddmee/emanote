## Scaling for clustering - normalisation

Background [[2022-03-21_0813_feature-vector]]

Most of the time we use some variant of the [Minkowski Metric](https://mathworld.wolfram.com/MinkowskiMetric.html).

![[2022-03-21_0824_minkowski-metric]]

```
The distance between two vectors x1 and x2, P is the degree we're going to be using. This equals...

The absolute difference between x1 - x2 raised to the power of p. Sum them, then take the 1/p.
```

For example if p is set to 2, that's the mean squared.

Also commonly used is setting p to 1. That's called the manhattan distance. Manhattan is laid out in a grid. If you want to go from top-left to bottom-right, you can't take the diagonal. You have to go down 1, right one, down 1, right one, etc. That's the manhattan distance.

![[2022-03-21_0837_manhattan-distance.jpeg]]

![[2022-03-21_0838_manhattan-euclidean.jpeg]]

#algorithms
#optimisation
#machinelearning
#supervised
#unsupervised
#clustering
