---
layout:     post
title:      "Time Series Analysis 2 ARCH examples"
category:   DataMining 
tags:       DataMining
---
* content
{:toc}

```python
# -*- coding:utf-8 -*-
# arch 模型的建立
# 步骤（1）：通过检验数据的序列相关性建立一个均值方程，如有必要，对收益率序列建立一个计量经济模型（如ARMA）来消除任何线形依赖。
# 步骤（2）：对均值方程的残差进行ARCH效应检验
# 步骤（3）：如果具有ARCH效应，则建立波动率模型
# 步骤（4）：检验拟合的模型，如有必要则进行改进
import pandas as pd
from statsmodels.tsa.stattools import adfuller
from statsmodels.tsa.arima_model import ARIMA
import matplotlib.pylab as plt
import numpy as np
from statsmodels.tsa.stattools import acf, pacf
import statsmodels.tsa as sm_tsa
import arch

dateparse = lambda dates: pd.datetime.strptime(dates, '%Y-%m')
data = pd.read_csv('AirPassengers.csv', index_col='Month',date_parser=dateparse)
ts = data['#Passengers']

# step 1: 检查平稳性，是否需要差分。 原假设H0：序列为非平稳的，备择假设H1:序列是平稳的
t = adfuller(ts)
print "p-value: ", t[1]
# 其结果是p-value:  0.991880243438，序列是非平稳的，进行差分
ts_diff = ts - ts.shift()
ts_diff.dropna(inplace=True)
t_diff = adfuller(ts_diff)
print "p-value after diff: ", t_diff[1]
# 其结果是p-value after diff:  0.0542132902838，拒绝原假设，序列是平稳的，接下来建立AR(p)模型
# 此处我们直接借用之前的结果ARIMA(2，1，2)
model = ARIMA(ts_diff, order=(2, 1, 2)).fit(disp=-1)

# step 2: ARCH效应检验
#　混成检验（Ljung-Box),检验序列{at^2}的相关性，来判断是否具有ARCH效应, 计算均值方差残差
# 绘制残差以及残差的平方
at = ts_diff -  model.fittedvalues
at2 = np.square(at)
plt.figure(figsize=(10,6))
plt.subplot(211)
plt.plot(at,label = 'at')
plt.legend()
plt.subplot(212)
plt.plot(at2,label='at^2')
plt.legend(loc=0)
plt.show()
#　然后对{at^2}序列进行混成检验： 原假设H0:序列没有相关性，备择假设H1：序列具有相关性
at2.dropna(inplace = True)
m = 25 # 我们检验25个自相关系数
acf,q,p = acf(at2,nlags=m,qstat=True)  ## 计算自相关系数 及p-value
out = np.c_[range(1,26), acf[1:], q, p]
output=pd.DataFrame(out, columns=['lag', "AC", "Q", "P-value"])
output = output.set_index('lag')
print output
# p-value小于显著性水平0.05，我们拒绝原假设，即认为序列具有相关性。因此具有ARCH效应。

# step3: 验证存在ARCH效应，建立ARCH模型
# 先通过{at^2}序列的偏自相关函数PACF来确定ARCH的阶次
lag_pacf = pacf(at2, nlags=30, method='ols')
plt.plot(lag_pacf)
plt.show()
# 大概突破的阶层应该是2，所以波动率模型选择ARCH(2)
train = ts_diff[:-10]
test = ts_diff[-10:]
am = arch.arch_model(train,mean='AR',lags=8,vol='ARCH',p=4)
res = am.fit()
print res.summary()
print res.params

# step 4: 检验拟合的模型
res.hedgehog_plot()
plt.show()


# GARCH(m,s)的定阶较难，一般使用低阶模型如GARCH(1,1),GARCH(2,1),GARCH(1,2)
am2 = arch.arch_model(train, mean='AR', lags=8, vol='GARCH')
res2 = am2.fit()
print res2.summary()
print res2.params
res2.hedgehog_plot()
plt.show()

## 后面则可进行波动率的预测
```