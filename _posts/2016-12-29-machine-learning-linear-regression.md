---
layout:     post
title:      "Simple Linear Regression Model"
category:   DataMining 
tags:		DataMining Python
---

* content
{:toc}

## About Linear Regression
Regression is a data mining function that predicts a number. A regression task begins with a data set in which the target values are known. The simplest form of regression to visualize is linear regression with a single predictor. 

## Preparing Data for Linear Regression

Linear Assumption. Linear regression assumes that the relationship between your input and output is linear. It does not support anything else. This may be obvious, but it is good to remember when you have a lot of attributes. You may need to transform data to make the relationship linear (e.g. log transform for an exponential relationship).

Remove Noise. Linear regression assumes that your input and output variables are not noisy. Consider using data cleaning operations that let you better expose and clarify the signal in your data. This is most important for the output variable and you want to remove outliers in the output variable (y) if possible.

Remove Collinearity. Linear regression will over-fit your data when you have highly correlated input variables. Consider calculating pairwise correlations for your input data and removing the most correlated.

Gaussian Distributions. Linear regression will make more reliable predictions if your input and output variables have a Gaussian distribution. You may get some benefit using transforms (e.g. log or BoxCox) on you variables to make their distribution more Gaussian looking.

Rescale Inputs: Linear regression will often make more reliable predictions if you rescale input variables using standardization or normalization.

## How does Linear Regression Work?

In mathematical notion, if \hat{y} is the predicted value.

![](/images/ML/linear_fomula.png)

In scikit-linear package, designate the vector w = (w_1,..., w_p) as coef_ and w_0 as intercept_.

LinearRegression fits a linear model with coefficients w = (w_1, ..., w_p) to minimize the residual sum of squares between the observed responses in the dataset, and the responses predicted by the linear approximation. Mathematically it solves a problem of the form:

![](/images/ML/linear_square.png)

## Test Linear Regression

Root Mean Squared Error

![](/images/ML/linear_RMSE.png)

Mean Absolute Error

![](/images/ML/linear_MAE.png)