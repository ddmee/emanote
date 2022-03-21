# K means clustering

[K-means clustering](https://en.wikipedia.org/wiki/K-means_clustering) is a form of [[2022-03-17_1012_clustering|clustering]].

It's a fast algorithm, roughly linearly to the size of the input.

Steps:

1. Choose K. K is the total number of clusters you want when you're finished.
2. Choose K points as initial centroids. These are often choosen at random.
3. Assign each point to the nearest centroid. (No reason to think inital assignment will give any useful clustering.)
4. For each cluster, choose a new centroid.
5. Assign each point to nearest centroid (getting a new clustering).
6. Repeat 4 & 5 until the change is small.

## What's a centroid?

See [[2022-03-21_1043_centroid]]

## Complexity

For each iteration, e.g. step 3, have to make `Kn` comparison, where n is the number of points. (Compare each point to each centroid.) Then the question is how many iterations (e.g. step 6) we have to do. Apparently this typically is a small number... Typically it's not proportional to N.

#algorithms
#optimisation
#machinelearning
#unsupervised
#clustering
