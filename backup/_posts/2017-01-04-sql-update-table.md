 ---
layout:     post
title:      SQL Update Table Operations
category:   [SQL] 
tags:       [SQL]
---

It compiles in Postgre SQL.

{% highlight SQL %}
-- add a column
alter table cece_table add name varchar(100);

-- update column name
alter table cece_table rename column name to another_name

-- update the values in one columns
update cece_table set name = '个人' where length(number) < 4;
update cece_table set name = table2.name 
from table2
where cece_table.id = table2.id;

-- delete some rows
delete from cece_table where id in (select id from table2)
{% endhighlight %}