---
layout:     post
title:      Feature Selection in Data Mining 
category:   [DataMining] 
tags:       [Data Mining]
---

Feature Selection

Scikit-learn provides some feature selection methods for data mining.

* Remove features with low variance

For discrete values, for example, one feature with two values ( 0 and 1 ), if there are more than 80% samples with the same values, then the feature is invalid, so we remove this feature.

As an example, suppose that we have a dataset with boolean features, and we want to remove all features that are either one or zero (on or off) in more than 80% of the samples. Boolean features are Bernoulli random variables, and the variance of such variables is given by

VAR[X] = p(1-p)

here we select p as 0.8

{% highlight Python %}
from sklearn.feature_selection import VarianceThreshold

# varriance threshould
X = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [0, 1, 0], [0, 1, 1]]
sel = VarianceThreshold(threshold=(.8*(1-.8)))
print sel.fit_transform(X)
{% endhighlihgt %}

the result removes the first column, which has a probability p = 5/6 > .8 of containing a zero.

* Univariate feature selection

Univariate feature selection works by selecting the best features based on univariate statistical tests. It can be seen as a preprocessing step to an estimator. 





