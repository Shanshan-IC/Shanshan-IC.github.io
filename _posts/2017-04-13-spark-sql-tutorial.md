---
layout:     post
title:      "Spark SQL Tutorial"
category:   Spark
tags:   Spark
---

* content
{:toc}

## Overview

Spark SQL is a Spark module for structured data processing. 

**SQL**

One use of Spark SQL is to execute SQL queries. Spark SQL can also be used to read data from an existing Hive installation. When running SQL from within another programming language the results will be returned as a Dataset/DataFrame. 

** Datasets and DataFrames
A Dataset is a distributed collection of data.  The Dataset API is available in Scala and Java. 

A DataFrame is a Dataset organized into named columns. It is conceptually equivalent to a table in a relational database or a data frame in R/Python, but with richer optimizations under the hood. DataFrames can be constructed from a wide array of sources such as: structured data files, tables in Hive, external databases, or existing RDDs. The DataFrame API is available in Scala, Java, Python, and R. In Scala and Java, a DataFrame is represented by a Dataset of Rows. In the Scala API, DataFrame is simply a type alias of Dataset[Row]. While, in Java API, users need to use Dataset<Row> to represent a DataFrame.


## Get Start

**Starting Point: SparkSession**

```scala
import org.apache.spark.sql.SparkSession

val spark = SparkSession
  .builder()
  .appName("Spark SQL basic example")
  .config("spark.some.config.option", "some-value")
  .getOrCreate()

// For implicit conversions like converting RDDs to DataFrames
import spark.implicits._
```

**Create Dataframe**
``scala
val df = spark.read.json("examples/src/main/resources/people.json")

// Displays the content of the DataFrame to stdout
df.show()
```

**Dataframe Operations**

```scala
import spark.implicits._
df.printSchema()
//select "name" column
df.select("name").show()
df.select($"name", $"age" + 1).show()
//filter
df.filter($"age" > 21).show()
//groupby count
df.groupBy("age").count().show()
```

For more operations, you can see the [Dataset AIP](http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.sql.Dataset)























