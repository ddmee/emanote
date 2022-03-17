# Machine Learning (ml)

ML is inductive inference.

The program observes examples that represent incomplete information about some statistical phenoma and then tries to generate a model that summarises some statistical property of the data and can be used to predict unseen data.

There are roughly two distinct approachs to ML: supervised and unsupervised learning.

## Supervised learning

In supervised learning: associate a label with each example in a training set. If the label is discrete we typically call it a classification problem. If the label is continuous, call it a regression problem. Goal is to generalise from the training set to predict things we haven't seen.

For example, let's say we are trying to work out what makes a dot a red dot versus a blue dot. What's the difference between them? The information is the x/y values and the labels are red or blue.

![[2022-03-17_0841_red-blue-dots-1.png]]

How would we tackle this problem? Questions:

- Are the labels accurate?
- Is the past representative of the future? Note, sometimes it is for a while then something in the environment changes, and now the model isn't going to predict well anymore.
- Do you have enough (training) data to generalise?
- Feature extraction. Deciding what features we're going to consider.
- How tight should be fit be?

From the example, we can look at two different ways we might classify the problem. We're typically looking for ways to divide the data in classification problems.

![[2022-03-17_0849_red-blue-dots-2.png]]

We do might do draw a triangle because it minimises the training error. If we looked at it as an [[2022-03-16_1635_optimisation-problems|optimisation problem]] we could say are objective function is to maximise the number of red points in the drawn area. And this shape would mean we've maximised that, minimising the training error. But is it overfit? Will it generalise well to future data?

Instead we could choose the linear. It doesn't minimise the training error but is it more predictive of future dots?

We don't really know what is the better result because the utility we're aiming for is predicting the future data which we obviously don't have. Perhaps we need more training data.

## Unsupervised learning

The big difference here is we having training data but no labels. It's like looking at the picture without knowing which are red or blue. So what can we learn? Typically we are learning about regularities of the data. This normally means clustering the data.

See [[2022-03-17_1012_clustering]]


#algorithms
#optimisation
#machinelearning
#supervised
#unsupervised
#clustering
