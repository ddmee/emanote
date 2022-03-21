# Feature vector

Something that incorporates multiple features for some data.

How do we deal with clustering something if there we want to cluster using more than one characteristic. Lets say we want to compare cities using the distance and the tempature.

A 'feature' is a vector of numbers that ca. One element can represent the distance in miles, the other represents the temperature.

But how do we compare across these two features? The numbers mean quite different things: temperature and distance. 20 miles isn't far between cities but it's a big temperature difference. What metric would we use? And would we need to consider scaling elements of the vector, to make the quantities of the different features equivalent enough to cluster.

Feature selection is critical to the outcome. It is where most of the thinking ends up going.

## How do we do scaling?

See [[2022-03-21_0816_scaling-normalisation]]

## Nominal categories

So far we've talked about things that are comparable, where each element of the feature vector can be represented as a floating point number. But we often need to deal with nominal (names) categories rather than numbers. Let's say we cluster people on eye colour or hair colour.

Typically we convert the category to a number and have some way to relate the numbers. We might convert blue to 0, green to 0.5 and brown 1. Indicating brown is further from blue than green. (Just an example, who knows why we'd think that. It depends on the domain.) These are fairly judgmental questions rather than pure math.

Often we contrive to have all the features ranging between 0 and 1, and then compare that.

See also [[2022-03-21_0903_clustering-mammals-example]]

#algorithms
#optimisation
#machinelearning
#supervised
#unsupervised
#clustering
