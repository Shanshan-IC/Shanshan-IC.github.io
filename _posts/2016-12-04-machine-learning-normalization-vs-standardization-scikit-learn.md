---
layout:     post
title:      Data Normalization vs Standardization
category:   [DataMining] 
tags:		[Data Mining]
---

To normalize data, all data values will take on a value of 0 to 1.  Since some models collapse at the value of zero, sometimes an arbitrary range of say 0.1 to 0.9 is chosen instead, but for this post I will assume a unity-based normalization. The following equation is what should be used to implement a unity-based normalization:

![](/images/ML/Normalize.jpg)

If you desire to have a more centralized set of normalized data, with zero being the central point, then the following equation can be used:

![](/images/ML/Normalize2.jpg)

To standardize your data, you will want the data to reflect how many standard deviations from the average that that data lies, with the following normal distribution curve representing the probability of each standard deviation for a normal distribution. The Z-Score is what will be calculated to standardize the data, and it reflects how many standard deviations from the average that the data point falls.

![](/images/ML/scales.png)

To determine the Z-Score of each data point, the following equation should be used:

![](/images/ML/Standardize.jpg)

Normalized and Standardized can be used to remove their scale from the models. However, standardizing is the preferred method because it produces meaningful information about each data point, and where it falls  within its normal distribution, plus provides a crude indicator of outliers.

