---
layout:     post
title:      Machine Learning Logistic Regression 
category:   [DataMining] 
tags:       [Data Mining]
---

* Why Logistic Regression?

Simple logistic regression is analogous to linear regression, except that the dependent variable is nominal, not a measurement. One goal is to see whether the probability of getting a particular value of the nominal variable is associated with the measurement variable; the other goal is to predict the probability of getting a particular value of the nominal variable, given the measurement variable.

*  The Binomial Distribution

We consider first the case where the response yi
is binary, assuming only two
values that for convenience we code as one or zero. For example, we could
define

![](/images/ML/binomialDistribution.png)

* How Does Logistic Regression Work?

Step 1: To Find hypothesis function

We use Sigmoid Function in this algorithm:

![](/images/ML/Sigmoid.png)

It has beautiful "S" shape:

![](/images/ML/SigmoidSshape.png)

The left one is linear decision border, The right one is non-linear decision border:

![](/images/ML/logisticBorder.png)

For linear decision border, the formula is:

![](/images/ML/logistic1.png)

![](/images/ML/logistic2.png)

Function h(X) has special meaning, it means the probability of the result is 1,

![](/images/ML/logistic3.png)

Step 2: To create Cost Function and J Function

It is calculated based on maximum likelihood method

![](/images/ML/logistic4.png)

Step 3: To get minimum J function and get the parameter theta

Use Gradient Descent:

Update theta 

![](/images/ML/logistic5.png)

So it is:

![](/images/ML/logistic6.png)

