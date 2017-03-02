---
layout:     post
title:      "Feature Selection in Data Mining"
category:   DataMining 
tags:       DataMining
---
* content
{:toc}

Feature Selection

Scikit-learn provides some feature selection methods for data mining.

Method 1: Remove features with low variance

For discrete values, for example, one feature with two values ( 0 and 1 ), if there are more than 80% samples with the same values, then the feature is invalid, so we remove this feature.

As an example, suppose that we have a dataset with boolean features, and we want to remove all features that are either one or zero (on or off) in more than 80% of the samples. Boolean features are Bernoulli random variables, and the variance of such variables is given by

VAR[X] = p(1-p)

here we select p as 0.8

```python
from sklearn.feature_selection import VarianceThreshold

# varriance threshould
X = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [0, 1, 0], [0, 1, 1]]
sel = VarianceThreshold(threshold=(.8*(1-.8)))
print sel.fit_transform(X)
```

the result removes the first column, which has a probability p = 5/6 > .8 of containing a zero.

Method 2: Univariate feature selection

Univariate feature selection works by selecting the best features based on univariate statistical tests. It can be seen as a preprocessing step to an estimator. 

In scikit-learn, it includes:

* SelectKBest: removes all but the k highest scoring features

* SelectPercentile: removes all but a user-specified highest scoring percentage of features

* GenericUnivariateSelect: allows to perform univariate feature selection with a configurable strategy. 

SelectKBest method example

```python
from sklearn.datasets import load_iris
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import chi2

iris = load_iris()
x, y = iris.data, iris.target
print x.shape
x_new = SelectKBest(chi2, k=2).fit_transform(x, y)
print x_new.shape
```

For the object, we can 

* For regression: f_regression, mutual_info_regression

* For classification: chi2, f_classif, mutual_info_classif

The methods based on F-test estimate the degree of linear dependency between two random variables. On the other hand, mutual information methods can capture any kind of statistical dependency, but being nonparametric, they require more samples for accurate estimation.

f_regression will calculate the p-value of features. Smaller noise, higher relationship lower p-value.

mutual_info_regression and mutual_info_classif are mutual information, sensitive to the discrete info.

Method 3: Feature selection using SelectFromModel

SelectFromModel is a meta-transformer that can be used along with any estimator that has a coef_ or feature_importances_ attribute after fitting. The features are considered unimportant and removed, if the corresponding coef_ or feature_importances_ values are below the provided threshold parameter. Apart from specifying the threshold numerically, there are built-in heuristics for finding a threshold using a string argument. Available heuristics are “mean”, “median” and float multiples of these like “0.1*mean”.

* L1-based feature selection

Linear models penalized with the L1 norm have sparse solutions: many of their estimated coefficients are zero. When the goal is to reduce the dimensionality of the data to use with another classifier

```python
# selection from model : linear model
from sklearn.svm import LinearSVC
from sklearn.feature_selection import SelectFromModel
lsvc = LinearSVC(C=0.01, penalty="l1", dual=False).fit(x, y)
model = SelectFromModel(lsvc, prefit=True)
x_new = model.transform(x)
print x_new.shape
```
