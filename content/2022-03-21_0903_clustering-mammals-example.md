## Clustering Mammals Example

Objective, let's cluster mammals on what they eat. 

Let's do this without knowing anything directly about what they eat. Often in (unsupervised) [[2022-03-17_0840_machine-learning]] we are trying to learn about something when we only have indirect or limited data on the matter. Let's say we don't have any labels about what mammals eat. But instead we have data about the mammals themselves. And we start with the hypthoesis that a mammals eating habits can be inferred from their dental records.

```
# Map of the Number of kinds of teeth, at each digit in the map.
C1='Right Top Incisors'
C2='Right Bottom Incisors'
C3='Right Top Canines'
C4='Right Bottom Canines'
C5='Right Top Premolars'
C6='Right Bottom Premolars'
C7='Right Top Molars'
```

| Mammal | Teeth Map |
| ------ | --------- |
| Brown Bat | 23113333 |
| Mole | 32103333 |
| Silver Hair Bat | 23112333 |
| Pigmy Bat | 23112233 |
| House Bat | 23111233 |
| Red Bat | 13112233 |
| Pika | 21002233 |
| Rabbit | 21003233 |
| Beaver | 11002133 |
| Groundhog | 11002133 |
| Marten | 33114412 |
| ... | ... |
| Moose | 04003333 |

## Let's cluster this... with hierarchical clustering

For background see [[2022-03-17_1020_hierarchical-clustering]]

Each tooth map is a feature vector, and we're going to iterate through all the clusters agglomerating the closest vectors.

```python
import pylab, random, string, copy

class Point(object):
    def __init__(self, name, originalAttrs, normalizedAttrs = None):
        """normalizedAttrs and originalAttrs are both arrays"""
        self.name = name
        self.unNormalized = originalAttrs
        if normalizedAttrs == None:
            self.attrs = originalAttrs
        else:
            self.attrs = normalizedAttrs
    def dimensionality(self):
        return len(self.attrs)
    def getAttrs(self):
        return self.attrs
    def getOriginalAttrs(self):
        return self.unNormalized
    def distance(self, other):
        #Euclidean distance metric
        result = 0.0
        for i in range(self.dimensionality()):
            result += (self.attrs[i] - other.attrs[i])**2
        return result**0.5
    def getName(self):
        return self.name
    def toStr(self):
        return self.name + str(self.attrs)
    def __str__(self):
        return self.name

class Cluster(object):
    def __init__(self, points, pointType):
        self.points = points
        self.pointType = pointType
        self.centroid = self.computeCentroid()
    def singleLinkageDist(self, other):
        minDist = self.points[0].distance(other.points[0])
        for p1 in self.points:
            for p2 in other.points:
                if p1.distance(p2) < minDist:
                    minDist = p1.distance(p2)
        return minDist
    def maxLinkageDist(self, other):
        maxDist = self.points[0].distance(other.points[0])
        for p1 in self.points:
            for p2 in other.points:
                if p1.distance(p2) > maxDist:
                    maxDist = p1.distance(p2)
        return maxDist
    def averageLinkageDist(self, other):
        totDist = 0.0
        for p1 in self.points:
            for p2 in other.points:
                totDist += p1.distance(p2)
        return totDist/(len(self.points)*len(other.points))
    def update(self, points):
        oldCentroid = self.centroid
        self.points = points
        if len(points) > 0:
            self.centroid = self.computeCentroid()
            return oldCentroid.distance(self.centroid)
        else:
            return 0.0
    def members(self):
        for p in self.points:
            yield p
    def isIn(self, name):
        for p in self.points:
            if p.getName() == name:
                return True
        return False
    def toStr(self):
        result = ''
        for p in self.points:
            result = result + p.toStr() + ', '
        return result[:-2]
    def __str__(self):
        names = []
        for p in self.points:
            names.append(p.getName())
        names.sort()
        result = ''
        for p in names:
            result = result + p + ', '
        return result[:-2]
    def getCentroid(self):
        return self.centroid
    def computeCentroid(self):
        dim = self.points[0].dimensionality()
        totVals = pylab.array([0.0]*dim)
        for p in self.points:
            totVals += p.getAttrs()
        centroid = self.pointType('mean',
                                   totVals/float(len(self.points)),
                                   totVals/float(len(self.points)))
        return centroid

class ClusterSet(object):
    def __init__(self, pointType):
        self.members = []
    def add(self, c):
        if c in self.members:
            raise ValueError
        self.members.append(c)
    def getClusters(self):
        return self.members[:]
    def mergeClusters(self, c1, c2):
        points = []
        for p in c1.members():
            points.append(p)
        for p in c2.members():
            points.append(p)
        newC = Cluster(points, type(p))
        self.members.remove(c1)
        self.members.remove(c2)
        self.add(newC)
        return c1, c2
    def findClosest(self, metric):
        minDistance = metric(self.members[0], self.members[1])
        toMerge = (self.members[0], self.members[1])
        for c1 in self.members:
            for c2 in self.members:
                if c1 == c2:
                    continue
                if metric(c1, c2) < minDistance:
                    minDistance = metric(c1, c2)
                    toMerge = (c1, c2)
        return toMerge    
    def mergeOne(self, metric, toPrint = False):
        if len(self.members) == 1:
            return None
        if len(self.members) == 2:
            return self.mergeClusters(self.members[0],
                                      self.members[1])
        toMerge = self.findClosest(metric)
        if toPrint:
            print 'Merged'
            print '  ' + str(toMerge[0])
            print 'with'
            print '  ' + str(toMerge[1])
        self.mergeClusters(toMerge[0], toMerge[1])
        return toMerge
    def mergeN(self, metric, numClusters = 1, history = [],
               toPrint = False):
        assert numClusters >= 1
        while len(self.members) > numClusters:
            merged = self.mergeOne(metric, toPrint)
            history.append(merged)
        return history
    def numClusters(self):
        return len(self.members) + 1
    def __str__(self):
        result = ''
        for c in self.members:
            result = result + str(c) + '\n'
        return result

#Mammal's teeth example
class Mammal(Point):
    def __init__(self, name, originalAttrs, scaledAttrs = None):
        Point.__init__(self, name, originalAttrs, originalAttrs)
    def scaleFeatures(self, key): 
        scaleDict = {'identity': [1,1,1,1,1,1,1,1],
                     '1/max': [1/3.0,1/4.0,1.0,1.0,1/4.0,1/4.0,1/6.0,1/6.0]}
        scaledFeatures = []
        features = self.getOriginalAttrs()
        for i in range(len(features)):
            scaledFeatures.append(features[i]*scaleDict[key][i])
        self.attrs = scaledFeatures

def readMammalData(fName):
    dataFile = open(fName, 'r')
    teethList = []
    nameList = []
    for line in dataFile:
        if len(line) == 0 or line[0] == '#':
            continue
        dataLine = string.split(line)
        teeth = dataLine.pop(-1)
        features = []
        for t in teeth:
            features.append(float(t))
        name = ''
        for w in dataLine:
            name = name + w + ' '
        name = name[:-1]
        teethList.append(features)
        nameList.append(name)
    return nameList, teethList

def buildMammalPoints(fName, scaling):
    nameList, featureList = readMammalData(fName)
    points = []
    for i in range(len(nameList)):
        point = Mammal(nameList[i], pylab.array(featureList[i]))
        point.scaleFeatures(scaling)
        points.append(point)
    return points
```

mammalTeeth.txt:

```text
#Number of kinds of teeth
#C1='Right Top Incisors'
#C2='Right Bottom Incisors'
#C3='Right Top Canines'
#C4='Right Bottom Canines'
#C5='Right Top Premolars'
#C6='Right Bottom Premolars'
#C7='Right Top Molars'
#C8='Right Bottom Molars'
   Brown Bat           23113333
   Mole                32103333
   Silver Hair Bat     23112333
   Pigmy Bat           23112233
   House Bat           23111233
   Red Bat             13112233
   Pika                21002233
   Rabbit              21003233
   Beaver              11002133
   Groundhog           11002133
   Gray Squirrel       11001133
   House Mouse         11000033
   Porcupine           11001133
   Wolf                33114423
   Bear                33114423
   Raccoon             33114432
   Marten              33114412
   Weasel              33113312
   Rat                 22000066
   Wolverine           33114412
   Badger              33113312
   River Otter         33114312
   Sea Otter           32113312
   Jaguar              33113211
   Cougar              33113211
   Fur Seal            32114411
   Sea Lion            32114411
   Grey Seal           32113322
   Elephant Seal       21114411
   Reindeer            04103333
   Elk                 04103333
   Deer                04003333
   Moose               04003333
   Dog                 33114423
   Human               22112233

```

Let's cluster hierarchically aiming for 2 clusters.

```python
#Use hierarchical clustering for mammals teeth
def test0(numClusters = 2, scaling = 'identity', printSteps = False,
          printHistory = True):
    points = buildMammalPoints('mammalTeeth.txt', scaling)
    cS = ClusterSet(Mammal)
    for p in points:
        cS.add(Cluster([p], Mammal))
    history = cS.mergeN(Cluster.maxLinkageDist, numClusters,
                        toPrint = printSteps)
    if printHistory:
        print ''
        for i in range(len(history)):
            names1 = []
            for p in history[i][0].members():
                names1.append(p.getName())
            names2 = []
            for p in history[i][1].members():
                names2.append(p.getName())
            print 'Step', i, 'Merged', names1, 'with', names2
            print ''
    clusters = cS.getClusters()
    print 'Final set of clusters:'
    index = 0
    for c in clusters:
        print '  C' + str(index) + ':', c
        index += 1
```

If you run it you get this output:

```text
>>> lec20.test0()
Step 0 Merged ['Beaver'] with ['Groundhog']
Step 1 Merged ['Gray Squirrel'] with ['Porcupine']
Step 2 Merged ['Wolf'] with ['Bear']
Step 3 Merged ['Marten'] with ['Wolverine']
Step 4 Merged ['Weasel'] with ['Badger']
Step 5 Merged ['Jaguar'] with ['Cougar']
Step 6 Merged ['Fur Seal'] with ['Sea Lion']
Step 7 Merged ['Reindeer'] with ['Elk']
Step 8 Merged ['Deer'] with ['Moose']
Step 9 Merged ['Dog'] with ['Wolf', 'Bear']
Step 10 Merged ['Brown Bat'] with ['Silver Hair Bat']
Step 11 Merged ['Pigmy Bat'] with ['House Bat']
Step 12 Merged ['Pika'] with ['Rabbit']
Step 13 Merged ['River Otter'] with ['Marten', 'Wolverine']
Step 14 Merged ['Sea Otter'] with ['Grey Seal']
Step 15 Merged ['Beaver', 'Groundhog'] with ['Gray Squirrel', 'Porcupine']
Step 16 Merged ['Reindeer', 'Elk'] with ['Deer', 'Moose']
Step 17 Merged ['Red Bat'] with ['Human']
Step 18 Merged ['Raccoon'] with ['Dog', 'Wolf', 'Bear']
Step 19 Merged ['Elephant Seal'] with ['Fur Seal', 'Sea Lion']
Step 20 Merged ['Weasel', 'Badger'] with ['Jaguar', 'Cougar']
Step 21 Merged ['Pigmy Bat', 'House Bat'] with ['Red Bat', 'Human']
Step 22 Merged ['Mole'] with ['Brown Bat', 'Silver Hair Bat']
Step 23 Merged ['River Otter', 'Marten', 'Wolverine'] with ['Sea Otter', 'Grey Seal']
Step 24 Merged ['House Mouse'] with ['Beaver', 'Groundhog', 'Gray Squirrel', 'Porcupine']
Step 25 Merged ['Weasel', 'Badger', 'Jaguar', 'Cougar'] with ['River Otter', 'Marten', 'Wolverine', 'Sea Otter', 'Grey Seal']
Step 26 Merged ['Raccoon', 'Dog', 'Wolf', 'Bear'] with ['Mole', 'Brown Bat', 'Silver Hair Bat']
Step 27 Merged ['Pika', 'Rabbit'] with ['Pigmy Bat', 'House Bat', 'Red Bat', 'Human']
Step 28 Merged ['Elephant Seal', 'Fur Seal', 'Sea Lion'] with ['Weasel', 'Badger', 'Jaguar', 'Cougar', 'River Otter', 'Marten', 'Wolverine', 'Sea Otter', 'Grey Seal']
Step 29 Merged ['Reindeer', 'Elk', 'Deer', 'Moose'] with ['Raccoon', 'Dog', 'Wolf', 'Bear', 'Mole', 'Brown Bat', 'Silver Hair Bat']
Step 30 Merged ['House Mouse', 'Beaver', 'Groundhog', 'Gray Squirrel', 'Porcupine'] with ['Pika', 'Rabbit', 'Pigmy Bat', 'House Bat', 'Red Bat', 'Human']
Step 31 Merged ['Elephant Seal', 'Fur Seal', 'Sea Lion', 'Weasel', 'Badger', 'Jaguar', 'Cougar', 'River Otter', 'Marten', 'Wolverine', 'Sea Otter', 'Grey Seal'] with ['Reindeer', 'Elk', 'Deer', 'Moose', 'Raccoon', 'Dog', 'Wolf', 'Bear', 'Mole', 'Brown Bat', 'Silver Hair Bat']
Step 32 Merged ['Rat'] with ['House Mouse', 'Beaver', 'Groundhog', 'Gray Squirrel', 'Porcupine', 'Pika', 'Rabbit', 'Pigmy Bat', 'House Bat', 'Red Bat', 'Human']

Final set of clusters:
  C0: Badger, Bear, Brown Bat, Cougar, Deer, Dog, Elephant Seal, Elk, Fur Seal, Grey Seal, Jaguar, Marten, Mole, Moose, Raccoon, Reindeer, River Otter, Sea Lion, Sea Otter, Silver Hair Bat, Weasel, Wolf, Wolverine
  C1: Beaver, Gray Squirrel, Groundhog, House Bat, House Mouse, Human, Pigmy Bat, Pika, Porcupine, Rabbit, Rat, Red Bat
```

So the question is, do you think these clusters make sense? Well, not really. It doesn't seem so. For example, most bat's are in C1 but some are in C2. Should they not be in the same cluster? Likewise a dog is in the same category as the deer. They seem different...

## Normalisation / scaling

What seems to be happening is some categories of teeth have a larger dynamic range than others. For example C1 ranges from 1 to 3, while C8 ranges from 0 to 6.

If you look at `buildMammalPoints()` there's a 'scaling' argument. This goes to the `class Mammal.scaleFeatures()` as a key which can either be 'identity' (no scaling) or `1/max` where max is the max size of each category.

If we call with scaling of '1/max', the clusters look like:

```
>>> test0(scaling='1/max')
...
Final set of clusters:
  C0: Badger, Bear, Brown Bat, Cougar, Dog, Elephant Seal, Fur Seal, Grey Seal, House Bat, Human, Jaguar, Marten, Mole, Pigmy Bat, Raccoon, Red Bat, River Otter, Sea Lion, Sea Otter, Silver Hair Bat, Weasel, Wolf, Wolverine
  C1: Beaver, Deer, Elk, Gray Squirrel, Groundhog, House Mouse, Moose, Pika, Porcupine, Rabbit, Rat, Reindeer

```

It seems like c0 is carnivors and c1 is herbivores. Anyway, scaling matters. And inference can work without labeling.

Notes and code from [MIT Opencourseware](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00sc-introduction-to-computer-science-and-programming-spring-2011/unit-3/lecture-20-more-clustering/)

#machinelearning
#unsupervised
#clustering
