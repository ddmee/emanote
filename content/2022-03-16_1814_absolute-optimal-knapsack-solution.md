# Absolute Optimal Knapsack Solution

How would be work out an absolute solution to the problem?

1. Represent each item by a pair. (It's value and weight.)
2. W as the maximum weight the knapsack can carry.
3. Represent the set of available items as a vector I.
4. Another vector V indicates whether the item in I has been taken. If `V[i] = 1, => (that implies) I[i] has been taken.` Whereas if `V[i] = 0, => I[i] hasn't been taken`.

With this formulation, we can go back to notion of an optimisation problem as a objective function with constraints.

The objective function to maximise: `Sum( V[i] * I[i] . value)`

This is why `V[i]` is either 0 or 1. As `I[i] . 0` is zero while `I[i] . 1` is i.

Subject to constraint: `Sum( V[i] * I[i] . weight ) <= W`

## How to implement this?

The brute-force solution would be:

1. Enumerate all possibilities.
2. Choose the best that meets the constraint.

How efficient is this? Well, how many possibilities are there in step 1? There are `2**n` possibilities. Where n is the number of items to select from.

#algorithms
#optimisation
#complexity
#npcomplete
#bruteforce
