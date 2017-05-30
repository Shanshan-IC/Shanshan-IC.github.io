---
layout:     post
title:      "Pig Tutorial"
category:   Spark 
tags:		Pig
---
* content
{:toc}

## Mode

```
# pig local mode 
pig -x local

# pig mapreduce mode
pig -x mapreduce
pig -x mapreduce Sample_script.pig
```

## load and store data

```
records= load 'hdfs://localhost:9000/input/sample_small.txt' using com.oserp.pigudf.WordCountLoadFunc() as (words:bag{word:(w:chararray)});

A = load '/data/cupid_algo/workspace/shanshan/dt=2017-04-16' using parquet.pig.ParquetLoader(); 
STORE records INTO ' hdfs://localhost:9000/pig_Output/ ' USING PigStorage (',');
```

## shell command, except cd

```
sh ls;

# clear the screen
clear;
```

## Diagnostic

```
# show the data
DUMP records;
# show the schema
DESCRIBE records;
# show the logical, physical relations
EXPLAIN records;
# execute step by step
ILLUSTRATE records;
```

## Group

```
# groupby
Group_data = GROUP records BY age;
Group_data = GROUP records BY (age, sex);
Group_all = GROUP records BY ALL;
# COGROUP two more relations
cogroup_data = COGROUP student_details by age, employee_details by age;
```

## Join

```
# inner join
Relation3_name = JOIN Relation1_name BY key, Relation2_name BY key ;
# left join
Relation3_name = JOIN Relation1_name BY id LEFT OUTER, Relation2_name BY customer_id;
# right join
outer_right = JOIN customers BY id RIGHT, orders BY customer_id;
# full join
outer_full = JOIN customers BY id FULL OUTER, orders BY customer_id;
# multiple key
emp = JOIN employee BY (id,jobid), employee_contact BY (id,jobid);
```

## Cross 向量积

```
Relation3_name = CROSS Relation1_name, Relation2_name;
```

## UNION, SPLIT, Distinct

```
student = UNION student1, student2;
SPLIT student_details into student_details1 if age<23, student_details2 if (22<age and age>25);
# delete the duplicate
distinct_data = DISTINCT student_details;
```

## Filter, Foreach, Order, Limit

```
# filter data
filter_data = FILTER student_details BY city == 'Chennai';
# for each
foreach_data = FOREACH student_details GENERATE id,age,city;
# get limited data
Result = LIMIT Relation_name required number of tuples;
# order
order_by_data = ORDER student_details BY age DESC;
```

## Functions

Pig-Latin AVG() 函数用于计算包内数值的平均值。在计算平均值时， AVG() 函数会忽略NULL值。

* 要获取全局平均值，我们需要执行Group All操作，并使用 AVG() 函数计算平均值。

* 要获取组的平均值，我们需要使用Group By运算符对其进行分组，然后继续使用average函数。

```
# eval func
student_gpa_avg = foreach student_group_all  Generate
# get average
student_gpa_avg = foreach student_group_all  Generate
   (student_details.firstname, student_details.gpa), AVG(student_details.gpa); 
# some functions
# bagtostring: transfer bag to string
# concat: two expressions
# MAX, MIN, COUNT, ISEMPTY, SUM, SUBTRACT
# TOBAG, TOTUPLE, TOMAP, TOP
# other string, numeric, date, time functions
## Execute pig Script

```
exec sample_script.pig
pig -x mapreduce hdfs://localhost:9000/pig_data/Sample_script.pig 
```