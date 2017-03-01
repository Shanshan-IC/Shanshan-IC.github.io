 ---
layout:     post
title:      SQL Errors Summary
category:   [SQL] 
tags:       [SQL]
---

mysql Error 

Error Code: 1046. No database selected Select the default DB to be used by double-clicking its name in the SCHEMAS list in the sidebar

You have to tell sql which database you are going to use.

{% highlight SQL %}
show databases;
USE mysql;
{% endhighlight %}