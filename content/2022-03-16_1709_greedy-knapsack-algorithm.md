# Greedy Knapsack Algorithm

See the [[2022-03-16_1646_knapsack-problem]]

Per [[2022-03-16_1704_greedy-algorithm]], use an iterative approach to pick the best locally optimal option.

Make the best choice of item to put in the knapsack. Then ask if you have remaining weight. Make the next best choice. Etc, until there's no room left for more items.

## How do we know the locally optimal choice at each step?

Well, to choose the local optimum we could:

1. rank the options to get their weight to value ratio (weight/value). Then at each step we'd choose the item with the highest ratio. Or;
2. choose the item with the lowest weight at each step. Or;
3. choose the item with the highest value at each step.

However, there's no guarantee this will give us the **best** solution all the time. And in fact, none of those options are always going to perform better than any other.

## How efficient is this algorithm?

Well, we need to first sort the items on the different values we care about. In this case, weight and value. So, that's `O(2 nlogn)`. Then once we've sorted it, we iterate through the items at most n times. So `O(n)`.

Given `O(nlogn)` is the largest term, that's the cost of the greedy algorithm.

#algorithms
#optimisation
#greedy
