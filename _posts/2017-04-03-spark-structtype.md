---
layout:     post
title:      "StructType for Spark to create a DataFrame"
category:   Spark
tags:   Spark
---

* content
{:toc}

It is from [stack overflow](http://stackoverflow.com/questions/31615657/how-to-add-a-new-struct-column-to-a-dataframe)

## StructType

I assume you start with some kind of flat schema like this:

```
root
 |-- lat: double (nullable = false)
 |-- long: double (nullable = false)
 |-- key: string (nullable = false)
```

First lets create example data:

```scala
import org.apache.spark.sql.Row
import org.apache.spark.sql.functions.{col, udf}
import org.apache.spark.sql.types._

val rdd = sc.parallelize(
    Row(52.23, 21.01, "Warsaw") :: Row(42.30, 9.15, "Corte") :: Nil)

val schema = StructType(
    StructField("lat", DoubleType, false) ::
    StructField("long", DoubleType, false) ::
    StructField("key", StringType, false) ::Nil)

val df = sqlContext.createDataFrame(rdd, schema)
```

An easy way is to use an udf and case class:

```scala
case class Location(lat: Double, long: Double)
val makeLocation = udf((lat: Double, long: Double) => Location(lat, long))

val dfRes = df.
   withColumn("location", makeLocation(col("lat"), col("long"))).
   drop("lat").
   drop("long")

dfRes.printSchema
```

and we get

```s
root
 |-- key: string (nullable = false)
 |-- location: struct (nullable = true)
 |    |-- lat: double (nullable = false)
 |    |-- long: double (nullable = false)
 ```

A hard way is to transform your data and apply schema afterwards:

```scala
val rddRes = df.
    map{case Row(lat, long, key) => Row(key, Row(lat, long))}

val schemaRes = StructType(
    StructField("key", StringType, false) ::
    StructField("location", StructType(
        StructField("lat", DoubleType, false) ::
        StructField("long", DoubleType, false) :: Nil
    ), true) :: Nil 
)

sqlContext.createDataFrame(rddRes, schemaRes).show
```

and we get an expected output

```
+------+-------------+
|   key|     location|
+------+-------------+
|Warsaw|[52.23,21.01]|
| Corte|  [42.3,9.15]|
+------+-------------+
```
