---
layout:     post
title:      Some Python Annoying Staff
category:   [Python] 
tags:       [Python]
---

{% highlight Python %}
# Python Chinese comments
# -*- coding: utf-8 -*-

# python export csv Chinese Problems: 
df.to_csv(path+'\\'+filename+'.csv', encoding='gb18030', index=False)

# dataframe to list
company_list = companys.values.tolist()

# string output Chinese
str(company_list).replace('[', '').replace(']', '').decode('string_escape') 
{% endhighlight %}