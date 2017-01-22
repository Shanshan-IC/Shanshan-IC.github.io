---
layout:     post
title:      Class Imbalance
category:   [DataMining] 
tags:		[Data Mining, Python]
---

* Class Imbalance Problem

It is the problem in machine learning where the total number of a class of data (positive) is far less than the total number of another class of data

Oversampling and undersampling in data analysis are techniques used to adjust the class distribution of a dataset.

* Why is it a problem?

Most machine learning algorithms and works best when the number of instances of each classes are roughly equal. When the number of instances of one class far exceeds the other, problems arise. 

* How to deal with this problem?

Cost function based approaches

The intuition behind cost function based approaches is that if we think one false negative is worse than one false positive, we will count that one false negative as, e.g., 100 false negatives instead. 

Sampling based approaches

This can be roughly classified into three categories:

1. Oversampling, by adding more of the minority class so it has more effect on the machine learning algorithm
2. Undersampling, by removing some of the majority class so it has less effect on the machine learning algorithm
3. Hybrid, a mix of oversampling and undersampling