# Hierarchical clustering

[Hierarchical clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering) is a form of [[2022-03-17_1012_clustering|clustering]].

![[2022-03-17_0858_red-blue-dots-3.png]]

Let's say we have n items to cluster. And let's assume we have an n by n distance matrix that tells us for each pair of items how far apart they are.

![[2022-03-17_1927_n-by-n-table.png]]

1. Start by assigning each item to it's own cluster. If we have n items, we now have n clusters.
2. Find the most similar pair of clusters, and merge them. (n-1 clusters).
3. Repeat step 2 as many times as desired.

In the table above, the most similar clusters by distance is BOS (boston) and NY (new york).

This is form of hierarhical clustering is called **agglomerative clustering**.

But how do we find the two most similar clusters at step 2? Especially after the clusters have multiple elements in them. We need to determine some metric to use. These are typically called **linkage criteria**.

## Single linkage/minimum method/connectedness

Consider the difference between clusters to be the shortest distance between any member of a cluster to any other member of a cluster. Shortest pair - the closest two points in two clusters. The best case.

## Complete Linkage/diameter/maximum

Consider the distance of clusters to be the maximum distance between any pairs of points in two clusters. Furtherest pair. The worst case.

## Other linkage criteria

Having tried the maximum or the minimum, unsurprisingly, you can use the average or median distance between clusters.

None of these criteria are neccessarily the *best* to use. They produce different results.

See [[2022-03-21_0903_clustering-mammals-example]]

#algorithms
#optimisation
#machinelearning
#unsupervised
#clustering
#agglomerative
#linkage
