---
layout: post
title:  "Hidden Markov Model Example in Python" 
categories: DataMining
tags:  DataMining
---

* content
{:toc}

## Codes

```python
# -*- coding:utf-8 -*-
from hmmlearn.hmm import GaussianHMM
import pandas as pd
import numpy as np
import matplotlib.pylab as plt

store_path = r"D:\Users\FUSHANSHAN863\Desktop\stock\data\stock.h5"
store = pd.HDFStore(store_path)
data = store['data_stock_raw_base']
store.close()
data.index = data['data_date']
# 每日最高最低价格的对数差值
logDel = np.log(np.array(data['thigh'])) - np.log(np.array(data['tlow']))
# 每5日的指数对数收益差
close = data['tclose']
logRet_1 = np.array(np.diff(np.log(close)))[4:]
logRet_5 = np.log(np.array(close[5:])) - np.log(np.array(close[:-5]))
# 每5日的指数成交量的对数差
volume = data['vaturnover']
logVol_5 = np.log(np.array(volume[5:])) - np.log(np.array(volume[:-5]))

# 三个特征合成
feature_select = np.column_stack([logDel[5:],logRet_5,logVol_5])

# HMM model
model = GaussianHMM(n_components=6, covariance_type="full", n_iter=2000).fit(feature_select)
hidden_stats = model.predict(feature_select)
Date = pd.to_datetime(data.index[5:])

plt.figure(figsize=(25, 18))
for i in range(model.n_components):
    pos = (hidden_stats==i)
    plt.plot_date(Date[pos],close[pos],'o',label='hidden state %d'%i,lw=2)
    plt.legend(loc="left")

plt.show()


# 为了测试隐藏状态分别表示什么，假设进行买入操作
res = pd.DataFrame({'Date':Date,'logRet_1':logRet_1,'state':hidden_stats}).set_index('Date')
plt.figure(figsize=(25, 18))
for i in range(model.n_components):
    pos = (hidden_stats==i)
    pos = np.append(0,pos[:-1])#第二天进行买入操作
    df = res.logRet_1
    res['state_ret%s'%i] = df.multiply(pos)
    plt.plot_date(Date,np.exp(res['state_ret%s'%i].cumsum()),'-',label='hidden state %d'%i)
    plt.legend(loc="left")

plt.show()


# 假设买入和卖空
buy = (hidden_stats == 0) + (hidden_stats == 5)

buy = np.append(0,buy[:-1])
sell = (hidden_stats == 1) + (hidden_stats == 3) \
        + (hidden_stats == 4) + (hidden_stats == 2)
sell = np.append(0,sell[:-1])
res['backtest_return'] = res.logRet_1.multiply(buy,axis = 0) \
                            - res.logRet_1.multiply(sell,axis = 0)
plt.figure(figsize = (15,8))
plt.plot_date(Date,np.exp(res['backtest_return'].cumsum()),'-',label='backtest result')
plt.legend()
plt.grid(1)
plt.show()
```