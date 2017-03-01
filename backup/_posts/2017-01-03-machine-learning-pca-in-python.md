---
layout:     post
title:      Principal Component Analysis Implemented in Python
category:   [DataMining] 
tags:       [Data Mining, Python]
---
Using Scikit-learn package
{% highlight Python %}
from sklearn.decomposition import PCA   
import numpy as np

data = np.read_csv('test.csv')
pca=PCA(n_components=3)
newData=pca.fit_transform(data) 

print pca.n_components
print pca.explained_variance_ratio_ 
{% endhighlight %}

Without packages
{% highlight Python %}
import numpy as np
# zero mean 零均值化，每个特征的均值都为0
def zeroMean(dataMat):
    meanVal = np.mean(dataMat, axis=0)
    newData = dataMat - meanVal
    return newData, meanVa

# pca function
def pca(dataMat, n):
    newData, meanVal = zeroMean(dataMat)
    # cov array
    covMat = np.cov(newData, rowvar= 0) # rowvar = 0 means one column presents one sample

    eigVals, eigVects = np.linalg.eig(np.mat(covMat))  # 求特征值和特征向量,特征向量是按列放的，即一列代表一个特征向量
    eigValIndice = np.argsort(eigVals)  # 对特征值从小到大排序
    n_eigValIndice = eigValIndice[-1:-(n + 1):-1]  # 最大的n个特征值的下标
    n_eigVect = eigVects[:, n_eigValIndice]  # 最大的n个特征值对应的特征向量
    lowDDataMat = newData * n_eigVect  # 低维特征空间的数据
    reconMat = (lowDDataMat * n_eigVect.T) + meanVal  # 重构数据
    return lowDDataMat, reconMat
{% endhighlight %}