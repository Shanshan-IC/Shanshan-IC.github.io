---
layout:     post
title:      "Spark Tutorial 1"
category:   Spark
tags:   Spark
---

* content
{:toc}

It is note when reading [Learn Spark](http://shop.oreilly.com/product/0636920028512.do)

```scala
//start
//绝对路径之前加上"file://"
var files = sc.textFile("file:///data/workspace/shanshan/test.md")
file.count()
file.first()

//Chapter 3 RDD
/*
弹性分布式数据集（RDD）。RDD 简单
来说就是元素的分布式集合。在 Spark 中，所有的工作都被表达为创建新 RDD，
对已存在的 RDD 做变换，或者对 RDD 调用某些操作来计算得到一个结果。在
底层，Spark 将包含在 RDD 中的数据自动分布到你的整个集群，并将你对其执
行的操作并行化。

用户可以用两种方式创建 RDD：通过加载一个外部数据集，或者在驱动程序中
分发一个对象集合（如 list 或 set）

RDD 一旦创建好了，可以提供两种不同类型的操作：变换(transformation)和动作
(action)。变换是从前一个 RDD 构造出一个新的 RDD。
*/

// 创建RDD
// 方式1：
// 将你程序中已存在的集合传递给 SparkContext 的 parallelize()方法
val lines = sc.parallelize(List(“pandas”, “i like pandas”))

// 更常见的方式是从外部存储加载数据
var files = sc.textFile("file:///data/workspace/shanshan/test.md")

// RDD操作，看返回类型判断是动作还是变换（返回RDD)
// 变换
var errors = files.filter(line=>line.contains("errors"))
files.collect()
// 动作
/*
它们是返回一个最终值给驱动程序或者写入外部存储系统的
操作。动作迫使对调用的 RDD 的变换请求进行求值，因为需要实际产生输出。
*/

// 延迟求值
/*
RDD 的变换是延迟求值，这意味着 Spark 直到看到一个动作才会进
行求值。*/

// 常用的RDD变换
/* map()变换传入
一个函数，并将该函数应用到 RDD 中的每一个元素。函数的返回结果就是变换
后的每个元素构成的新 RDD。filter()变换也是传入一个函数，返回的是该 RDD
中仅能通过该函数的元素构成的新 RDD。*/

// var, val, def
/*
def defines a method
val defines a fixed value (which cannot be modified)
var defines a variable (which can be modified)
*/
val input = sc.parallelize(List(1, 2, 3, 4))
val result = input.map(x => x * x)
println(result.collect().mkString(","))

//flipMap 返回返回值的迭代器
lines = sc.parallelize(["hello world", "hi"])
words = lines.flatMap(lambda line: line.split(" "))
words.first() # returns "hello"


// 伪集合操作
// 笛卡尔积，返回所有可能组合

// reduce 函数
/* 它传入一个函数，该函数对 RDD
中两个元素进行处理，并返回一个同类型的元素。*/
val sum = rdd.reduce((x, y) => x + y)

/* fold()函数和 reduce()函数类似，也是带了一个和 reduce()相同的函数参数，但是
多了一个“零值”用于在每个分区调用时初始化。

aggregate()函数将我们从被约束只能返回处理的 RDD 的相同类型 RDD 中解脱
了。aggregate()和 fold()一样有一个初始的零值，但是可以是我们想要返回的类型。
*/

val result = input.aggregate((0, 0))(
				(acc, value) => (acc._1 + value, acc._2 + 1),
				(acc1, acc2) => (acc1._1 + acc2._1, acc1._2 + acc2._2))
val avg = result._1 / result._2.toDouble


//数据到驱动程序
/* 
最简单最常用的返回数据到驱动程序的操作是 collect()，返回整个 RDD 的数据。
take(n)返回 RDD 中的 n 个元素，试图最小化访问的分区的数目。所以它返回的
是有偏差的集合。重要的是知道这操作不会以你期待的顺序返回数据
*/

/* 为避免多次计算同一个 RDD,我们可以要求 Spark 缓存该数据。当我们要求 Spark
缓存该 RDD 时，计算该 RDD 的节点都会保存它们的分区。*/
//使用persist

val result = input.map(x => x * x)
result.persist(StorageLevel.DISK_ONLY)
println(result.count())
println(result.collect().mkString(","))



// Chapter 4 Key/Value Pairs
/* 目的： Pair RDD 在许多程序中都是很有用的组件，因为它们对外的操作可以让
你并行的处理每个键，或者跨网络重组数据。例如，Pair RDD有一个reduceByKey()
的方法，它可以对每个键的数据分别进行聚合；join()方法可以通过对两个 RDD
中相同的元素进行分组合并。*/
// 创建RDD
// 可通过对已有的RDD进行map返回key/values
var pairs = files.map(x=>(x.split("")(0), x))
// 可通过调用SparkContext.parallelize(),从内存中的集合创建
//Pair RDD 允许使用标准 RDD 的所有转换。

// words count
val input = sc.textFile("s3://...")
val words = input.flatMap(x => x.split(" "))
val result = words.map(x => (x, 1)).reduceByKey((x, y) => x + y)

/* 要 理 解 combineByKey() ， 想 想 它 是 如 何 处 理 每 个 元 素 会 有 些 帮 助 。
combineByKey()会遍历一个分区中的所有元素。每个元素都有一个键，要么之间
54
没出息过，要么之前已经出现过。如果是新元素，combineByKey()会创建
combiner()，也就是我们提供给它的函数来为这个新的键创建初值用于累积计算。
这里有一点很重要，这个第一次是每个分区中新的键的第一次出现，而不是整个
RDD 第一次出现。
如果在这个分区这个键之前出现过，就对这个键进行多次累计就行了。当我们合
并各个分区的数据时，如果两个以上的分区对于同一个键都有累积值，可以用用
户提供的 mergeCombiner()合并即可。
*/

def
combineByKey[C](createCombiner: (V) => C, mergeValue: (C, V) => C, mergeCombiners: (C, C) => C): RDD[(K, C)]

val result = inputs.combineByKey(
(v) => (v, 1),
(acc: (Int, Int), v) => (acc._1 + v, acc._2 + 1),
(acc1: (Int, Int), acc2: (Int, Int)) => (acc1._1 + acc2._1, acc1._2 + acc2._2)
).map{ case (key, value) => (key, value._1 / value._2.toFloat) }



//调整并行级别
val data = Seq(("a", 3), ("b", 4), ("a", 1))
sc.parallelize(data).reduceByKey((x, y) => x + y) // Default parallelism
sc.parallelize(data).reduceByKey((x, y) => x + y) // Custom parallelism

/*有时我们需要对RDD 的分组或聚合操作的上下文之外来改变分区。对这些情况，
Spark 提供了repartition()函数。它可以跨网络对数据进行shuffle，并创建一组新
的分区。记住，对数据进行重新分区是一个相当昂贵的操作。Spark 也有一个
repartition()的优化版本叫做coalesce()。它可以避免数据移动，但是仅限于减少
RDD 的分区数的情况。*/

//有主键则可连接
storeAddress = {
(Store("Ritual"), "1026 Valencia St"), (Store("Philz"), "748 Van Ness Ave"),
(Store("Philz"), "3101 24th St"), (Store("Starbucks"), "Seattle")}
storeRating = {
(Store("Ritual"), 4.9), (Store("Philz"), 4.8))}
storeAddress.join(storeRating) == {
(Store("Ritual"), ("1026 Valencia St", 4.9)),
(Store("Philz"), ("748 Van Ness Ave", 4.8)),
(Store("Philz"), ("3101 24th St", 4.8))}
// 上面是内连接，还有leftOuterJoin(other)和rightOuterJoin(other)

//排序

val input: RDD[(Int, Venue)] = ...
implicit val sortIntegersByString = new Ordering[Int] {
override def compare(a: Int, b: Int) = a.toString.compare(b.toString)
}
rdd.sortByKey()

// 数据分区
val sc = new SparkContext(...)
val userData = sc.sequenceFile[UserID, UserInfo]("hdfs://...")
.partitionBy(new HashPartitioner(100)) // Create 100 partitions
.persist()

/*
processNewLogs()方法保持不变：对于processNewLogs()来说events RDD 是本地
的，并且只在这个方法里用到，所以对event RDD 指定分区不会有改善。因为在
构建userData 时我们调用了partitionBy()函数，这样Spark 就知道它是哈希分区
的，在执行join()时会利用这个信息。特别是在调用userData.join(events)的时候，
Spark 仅会对events RDD 进行shuffle，并根据UserID 将events 发送到userData
的哈希分区对应的机器上（见图4-5）。结果就是网络上传输的数据大量减少，
程序运行的明显快了
*/


// 加载和保存数据
//加载文本数据
val input = sc.textFile("file:///home/holden/repos/spark/README.md")
//保存
input.saveAsTextFile(outputFile)

//加载json
import com.fasterxml.jackson.module.scala.DefaultScalaModule
import com.fasterxml.jackson.module.scala.experimental.ScalaObjectMapper
import com.fasterxml.jackson.databind.ObjectMapper
import com.fasterxml.jackson.databind.DeserializationFeature

case class Person(name: String, lovesPandas: Boolean) // Must be a top-level class

// Parse it into a specific case class. We use flatMap to handle errors
// by returning an empty list (None) if we encounter an issue and a
// list with one element if everything is ok (Some(_)).
val result = input.flatMap(record => {
try {
Some(mapper.readValue(record, classOf[Person]))
} catch {
case e: Exception => None
}})

//过滤喜欢熊猫的人导入到JSON文件
result.filter(p => P.lovesPandas).map(mapper.writeValueAsString(_))
.saveAsTextFile(outputFile)

//textFile加载CSV

/*SequenceFile 是一种流行的Hadoop 文件格式，由一些带key/value 元组的无格式
文件组成。它具有同步标志，允许Spark 定位到文件中的某处后再次同步到记录
边界。这使得Spark 可以从多个节点高效的并行读取SequenceFile*/
val data = sc.sequenceFile(inFile, classOf[Text], classOf[IntWritable]).
map{case (x, y) => (x.toString, y.get())}
//保存SequenceFile
data.saveAsSequenceFile(outputFile)

//加载protocol文件

//加载压缩文件
val rdd = sc.textFile("file:///home/holden/happypandas.gz")

//加载HDFS
val rdd = sc.textFile("hdfs://master:port/path")

// HIVE data
import org.apache.spark.sql.hive.HiveContext
val hiveCtx = new org.apache.spark.sql.hive.HiveContext(sc)
val rows = hiveCtx.sql("SELECT name, age FROM users")
val firstRow = rows.first()
println(firstRow.getString(0)) // Field 0 is the name
```