---
layout:     post
title:      Principal Component Analysis
category:   [DataMining] 
tags:       [Data Mining]
---

* When is Principal Component Analysis needed?

	too many features

	most of features are correlated

	poor accuracy with too many data

* What is PCA?

PCA is a method of extracting import variables from a larget set data in dataset. It extracts low dimensional set of features from a high dimensional data with a motive to capture as much information as possible. 

A principal component is a normalized linear combination of the original predictors in a data set. 

Let’s say we have a set of predictors as X¹, X²...,Xp

The principal component can be written as:

	Z¹ = Φ¹¹X¹ + Φ²¹X² + Φ³¹X³ + .... +Φp¹Xp

where,

	Z¹ is first principal component
	
	Φp¹ is the loading vector comprising of loadings (Φ¹, Φ²..) of first principal component. The loadings are constrained to a sum of square equals to 1. This is because large magnitude of loadings may lead to large variance. It also defines the direction of the principal component (Z¹) along which data varies the most. It results in a line in p dimensional space which is closest to the n observations. Closeness is measured using average squared euclidean distance.
	
	X¹..Xp are normalized predictors. Normalized predictors have mean equals to zero and standard deviation equals to one.

* How to calculate it?



* Limitation

As noted above, the results of PCA depend on the scaling of the variables. A scale-invariant form of PCA has been developed.

* Codes in the next blog