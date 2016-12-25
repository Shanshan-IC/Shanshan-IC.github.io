---
layout:     post
title:      Data Mining Proprocessing in Python: Scaling
category:   [Data Mining] 
tags:		[Data Mining, Python]
---

The sklearn.preprocessing package provides several common utility functions and transformer classes.

* Standardization

Centering and scaling happen independently on each feature by computing the relevant statistics on the samples in the training set. Mean and standard deviation are then stored to be used on later data using the transform method.

In practice we often ignore the shape of the distribution and just transform the data to center it by removing the mean value of each feature, then scale it by dividing non-constant features by their standard deviation.

{% highlight Python %}
# scale : quick to do standarization
x = np.array([[ 1., -1.,  2.],
              [ 2.,  0.,  0.],
              [ 0.,  1., -1.]])
x_scale = preprocessing.scale(x)
print x_scale
# scale data has zero means and unit variance
print "Scale mean is \n", x_scale.mean(axis = 0)
print "Scale std is \n",x_scale.std(axis = 0)
{% endhighlight %}
The output is 

	[[ 0.         -1.22474487  1.33630621]
	 
	 [ 1.22474487  0.         -0.26726124]
	 
	 [-1.22474487  1.22474487 -1.06904497]]
	
	Scale mean is 
	
	[ 0.  0.  0.]
	
	Scale std is 
	
	[ 1.  1.  1.]

sklearn also provides sklearn.preprocessing.StandardScaler to compute the mean and standard deviation on a training set in case that training data uses the same transformation.

sklearn.preprocessing.StandardScaler(copy=True, with_mean=True, with_std=True)

	with_mean: If True, center the data before scaling.

	with_str: If True, scale the data to unit variance.

	copy: If False, try to avoid a copy and do inplace scaling instead. 

Attributes:
	scale_

	mean_

	var_

	n_samples_seen_: The number of samples processed by the estimator. 

StandardScaler Examples	
{% highlight Python %}
# sklearn.preprocessing.StandardScaler
scaler = preprocessing.StandardScaler().fit(x)

print "Mean is \n", scaler.mean_
print "Std is \n", scaler.std_
print "Scale is \n", scaler.scale_
print scaler.transform(x)
{% endhighlight %}
The output is 

	Mean is 
	
	[ 1.          0.          0.33333333]
	
	Std is 
	
	[ 0.81649658  0.81649658  1.24721913]
	
	Scale is 
	
	[ 0.81649658  0.81649658  1.24721913]
	
	[[ 0.         -1.22474487  1.33630621]
	
	 [ 1.22474487  0.         -0.26726124]
	
	 [-1.22474487  1.22474487 -1.06904497]]

* Scaling features to a range

An alternative standardization is scaling features to lie between a given minimum and maximum value. This can be achieved using MinMaxScaler or MaxAbsScaler, respectively.

MinMaxScaler transformation formula:

X_std = (X - X.min(axis=0)) / (X.max(axis=0) - X.min(axis=0))

X_scaled = X_std * (max - min) + min

sklearn.preprocessing.MinMaxScaler(feature_range=(0, 1), copy=True)[source]

Attributes: min_, scale_, data_min_, data_max_, data_range_

{% highlight Python %}
min_max_scaler = preprocessing.MinMaxScaler()
x_minmax = min_max_scaler.fit_transform(x)
print x_minmax
print "min_max_scaler scale is \n", x_minmax.scale_
print "min_max_scaler min is \n", x_minmax.min_
{% endhighlight %}
The output is 

	[[ 0.5         0.          1.        ]
	 
	 [ 1.          0.5         0.33333333]
	 
	 [ 0.          1.          0.        ]]
	
	min_max_scaler scale is 
	
	[ 0.5         0.5         0.33333333]
	
	min_max_scaler min is 
	
	[ 0.          0.5         0.33333333]

MaxAbsScaler works in a very similar fashion, but scales in a way that the training data lies within the range [-1, 1] by dividing through the largest maximum value in each feature. It is meant for data that is already centered at zero or sparse data.

sklearn.preprocessing.MaxAbsScaler(copy=True)

{% highlight Python %}
MaxAbsScaler
max_abs_scaler = preprocessing.MaxAbsScaler()
x_maxabs = max_abs_scaler.fit_transform(x)
print x_maxabs
print max_abs_scaler.scale_
{% endhighlight %}

* Scaling sparse data

Centering sparse data would destroy the sparseness structure in the data, and thus rarely is a sensible thing to do. However, it can make sense to scale sparse inputs, especially if features are on different scales.

MaxAbsScaler and maxabs_scale were specifically designed for scaling sparse data, and are the recommended way to go about this. However, scale and StandardScaler can accept scipy.sparse matrices as input, as long as with_mean=False is explicitly passed to the constructor. 

* Scaling data with outliers

If your data contains many outliers, scaling using the mean and variance of the data is likely to not work very well. In these cases, you can use robust_scale and RobustScaler as drop-in replacements instead. They use more robust estimates for the center and range of your data.

sklearn.preprocessing.robust_scale(X, axis=0, with_centering=True, with_scaling=True, quantile_range=(25.0, 75.0), copy=True)

class sklearn.preprocessing.RobustScaler(with_centering=True, with_scaling=True, quantile_range=(25.0, 75.0), copy=True)
