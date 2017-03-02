---
layout:     post
title:      "StatsModels Statistics Packages in Python with Time Series Analysis"
category:   DataMining 
tags:       DataMining
---
* content
{:toc}

Python Package StatsModels has the Time Series Analysis Module in tsa. Here we summary some frequently used in practice.

```python
# -*- coding:utf-8 -*-

import pandas as pd
from statsmodels.tsa.stattools import *
import matplotlib.pylab as plt
from statsmodels.tsa import ar_model
from statsmodels.tsa.vector_ar import var_model

dateparse = lambda dates: pd.datetime.strptime(dates, '%Y-%m')
data = pd.read_csv('AirPassengers.csv', index_col='Month',date_parser=dateparse)
ts = data['#Passengers']

# 1. Descriptive Statistics and Tests
#  自协方差
autocovariance_data =   acovf(ts)
# 自回归函数--可用于确定AR的阶层
acf_data = acf(ts, nlags=40)
# 部分自相关函数 -- 可用于确定MA的阶层
pacf_data = pacf(ts, nlags=40)
#　交叉协方差，两个样本的
crosscovariance_data = ccovf(ts, ts)
# 交叉相关矩阵，两个样本
crosscorrelation_data = ccf(ts, ts)
# ADF 检验，用于检验平稳性
# 返回值为['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used']
adf_res = adfuller(ts)
# Ljung-Box Q Statistic
qStat_data = q_stat(ts, nobs=20)


# 2. Estimation
# 单变量AR
model_AR = ar_model.AR(ts)
res_AR = model_AR.fit()
# 可查看更多内置函数
result_AR = ar_model.ARResults(model_AR, ts)
#　print result_AR.aic()
# ARMA 和ARIMA用法和AR函数相似
# ARMA,且ARMA process有专门的属性函数
model_ARMA = ar_model.ARMA(ts, order=(2,2))
# ARIMA
model_ARIMA = ar_model.ARIMA(ts, order=(2,1,2))
# VAR，详情见VARexample

# 3. ARMA Process
# 4. var
# 5. VARMA Process
# Time Series Filters

```

To see VAR and ARIMA full details, go to the post Time Series Analysis.