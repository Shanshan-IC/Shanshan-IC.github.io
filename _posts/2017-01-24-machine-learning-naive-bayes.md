---
layout:     post
title:      Machine Learning Naive Bayes
category:   [DataMining] 
tags:       [Data Mining]
---

Naive Bayes Algorithms

Part 1. The foundation: Probabilistic model

Abstractly, naive Bayes is a conditional probability model: given a problem instance to be classified. Bayes Probability terminology:

![](/images/ML/bayes1.png)

Part 2.  Knowledgement and Process

The sample belongs to the type with the highest probability. The definition is:

a. ![](/images/ML/bayes2.png) is the features data, a means x's every feature

b. Multiple classes: ![](/images/ML/bayes3.png)

c. Calculate conditional Probabilistic: ![](/images/ML/bayes4.png)

d. If ![](/images/ML/bayes5.png), then ![](/images/ML/bayes6.png)

The point is how to calculate the step c:

c.1 Get the training set.

c.2 Calculate the conditional probability:

![](/images/ML/bayes7.png)

c.3 If features are conditional dependent, based on

![](/images/ML/bayes8.png)

Because the denominator is constant, so maximum the numerator, and features are dependent, so

![](/images/ML/bayes9.png)

Part 3. Constructing a classifier from the probability model

The discussion so far has derived the independent feature model, that is, the naive Bayes probability model. The naive Bayes classifier combines this model with a decision rule. One common rule is to pick the hypothesis that is most probable; this is known as the maximum a posteriori or MAP decision rule. The corresponding classifier, a Bayes classifier, is the function that assigns a class label ![](/images/ML/bayes10.png) for some k as follows:

![](/images/ML/bayes11.png)

Part 4. Parameter estimation and event models

* Gaussian Naive Bayes



