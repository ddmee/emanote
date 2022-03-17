# Absolute Optimal/Brute Force Knapsack Solution

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

Here's some code:

```python
class Item(object):
    def __init__(self, n, v, w):
        self.name = n
        self.value = float(v)
        self.weight = float(w)
    def getName(self):
        return self.name
    def getValue(self):
        return self.value
    def getWeight(self):
        return self.weight
    def __str__(self):
        result = '<' + self.name + ', ' + str(self.value) + ', '\
                 + str(self.weight) + '>'
        return result

def buildItems():
    names = ['clock', 'painting', 'radio', 'vase', 'book',
             'computer']
    vals = [175,90,20,50,10,200]
    weights = [10,9,4,2,1,20]
    Items = []
    for i in range(len(vals)):
        Items.append(Item(names[i], vals[i], weights[i]))
    return Items

def dToB(n, numDigits):
    """Build a vector of items taken, represented as a string of binary numbers

    requires: n is a natural number less than 2**numDigits

    Returns a binary string of length numDigits representing the decimal number n."""
    assert type(n)==int and type(numDigits)==int and\
           n >=0 and n < 2**numDigits
    bStr = ''
    while n > 0:
        bStr = str(n % 2) + bStr
        n = n//2
    while numDigits - len(bStr) > 0:
        bStr = '0' + bStr
    return bStr

def genPset(Items):
    """Generate a list of lists representing the power set of Items"""
    numSubsets = 2**len(Items)
    templates = []
    for i in range(numSubsets):
        templates.append(dToB(i, len(Items)))
    pset = []
    for t in templates:
        elem = []
        for j in range(len(t)):
            if t[j] == '1':
                elem.append(Items[j])
        pset.append(elem)
    return pset

def chooseBest(pset, constraint, getVal, getWeight):
    """
    pset = a power set
    constraints = constraints
    getVal = a function that gets the value of an item
    getWeight = a function that gets weight of an item
    """
    bestVal = 0.0
    bestSet = None
    for Items in pset:
        ItemsVal = 0.0
        ItemsWeight = 0.0
        for item in Items:
            ItemsVal += getVal(item)
            ItemsWeight += getWeight(item)
        if ItemsWeight <= constraint and ItemsVal > bestVal:
            bestVal = ItemsVal
            bestSet = Items
    return (bestSet, bestVal)

def testBest():
    Items = buildItems()
    pset = genPset(Items)
    taken, val = chooseBest(pset, 20,
                            Item.getValue, Item.getWeight)
    print ('Total value of items taken = ' + str(val))
    for item in taken:
        print '  ', item
```

## What does this code do?

1. `dtoB()` produces a vector of taken items
2. `genPSet()` generates a [[2022-03-17_0800_power-sets|power set]] of every subset of items.

This means we now have all the possible combinations, but without yet obeying the constraints.

3. `chooseBest()` iterates through the powerset finding the set with the best value.

Note, there may be more than one optimal set. I.e. multiple sets with the highest value for the amount of weight allowed. `chooseBest()` will just return one of these sets.

Code from [MIT Opencourseware](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00sc-introduction-to-computer-science-and-programming-spring-2011/unit-2/lecture-19-more-optimization-and-clustering/)

![[https://github.com/ddmee/Grokking-the-Coding-Interview-Patterns/blob/main/knapsack.png]]

#algorithms
#optimisation
#complexity
#npcomplete
#bruteforce
