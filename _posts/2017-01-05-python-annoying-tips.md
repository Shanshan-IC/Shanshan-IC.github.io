---
layout:     post
title:      "Some Python Annoying Staff"
category:   Python 
tags:       Python
---

* content
{:toc}

```python
# Python Chinese comments
# -*- coding: utf-8 -*-

# UnicodeEncodeError: 'ascii' codec can't encode characters in position 
import sys
reload(sys)
sys.setdefaultencoding('utf8')

# python export csv Chinese Problems: 
df.to_csv(path+'\\'+filename+'.csv', encoding='gb18030', index=False)

# dataframe to list
company_list = companys.values.tolist()

# string output Chinese
str(company_list).replace('[', '').replace(']', '').decode('string_escape') 
```

# read csv with Chinese
df = pd.read_csv("data.csv", encoding = 'gbk')

# dataframe to dictionary
data = full_data.set_index('id')['values'].to_dict()

# set to list
l = list(set([0, 1, 2]))
```

