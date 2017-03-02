---
layout:     post
title:      "Python connects with SQL"
category:   SQL 
tags:		SQL Python
---
* content
{:toc}

Python connect with SQL to get the sql query result.

```python
import psycopg2
import sys
import pandas as pd
from sqlalchemy import create_engine
import os
import sqlalchemy

# pgSQL
engine1 = create_engine('postgresql+psycopg2://...') # including the sql username and password
# if connect with Oracle, for Chinese
os.environ['NLS_LANG'] = 'SIMPLIFIED CHINESE_CHINA.UTF8'

sql = "SQL QUERY LIKE SELECT ..."
# sometimes it may occur the situation:  sql 含转义字符, add one more line
sql = sqlalchemy.text(sql)
df = pd.read_sql_query(sql.engine1)
# df is the result of sql query
# pgSQL Chinese is fine, but for the Oracle or mySQL, it maybe be wrong, add one line
# for the chinese columns
name = name.encode('latin-1').decode('gbk') 
```