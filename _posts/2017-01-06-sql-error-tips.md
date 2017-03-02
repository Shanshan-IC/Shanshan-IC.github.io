 ---
layout:     post
title:      "SQL Errors Summary"
category:   SQL 
tags:       SQL
---
* content
{:toc}

mysql Error 

Error Code: 1046. No database selected Select the default DB to be used by double-clicking its name in the SCHEMAS list in the sidebar

You have to tell sql which database you are going to use.

```sql
show databases;
USE mysql;
```