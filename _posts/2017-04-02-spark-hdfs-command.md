---
layout:     post
title:      "Hadoop HDFS Command"
category:   Spark
tags:   Hadoop HDFS
---

* content
{:toc}

The Chinese one is from [hadoop HDFS常用文件操作命令](https://segmentfault.com/a/1190000002672666)

HDFS is the primary distributed storage used by Hadoop applications. A HDFS cluster primarily consists of a NameNode that manages the file system metadata and DataNodes that store the actual data. The HDFS Architecture Guide describes HDFS in detail. 

## Basic HDFS command

```
hadoop fs -cmd < args >
```

* ls

Files within a directory are order by filename by default.

```
hadoop fs -ls
hadoop fs -ls /data
```

* put

Copy single src, or multiple srcs from local file system to the destination file system. Also reads input from stdin and writes to destination file system.

```
hadoop fs -put < local file > < hdfs file >
hadoop fs -put - < hdsf  file> # read from keyboard to hdfs file, Ctrl+D to exit
```

* moveFromLocal

Similar to put command, except that the source localsrc is deleted after it’s copied.

```
hadoop fs -moveFromLocal  < local src > ... < hdfs dst >
```

* copyFromLocal

Similar to put command, except that the source is restricted to a local file reference.

```
hadoop fs -copyFromLocal  < local src > ... < hdfs dst >
```

* get

Copy files to the local file system.

```
hadoop fs -get < hdfs file > < local file or dir>
#the name of local's and hdfs cannot be the same
```

* copyToLocal

smiliar with get

```
hadoop fs -copyToLocal < local src > ... < hdfs dst >
```

* rm

remove file or directory

```
hadoop fs -rm < hdfs file > ...
hadoop fs -rm -r < hdfs dir>...
```

* mkdir

create directory

```
hadoop fs -mkdir < hdfs path>
```

* getmerge

Takes a source directory and a destination file as input and concatenates files in src into the destination local file. 

```
hadoop fs -getmerge < hdfs dir >  < local file >
hadoop fs -getmerge -nl  < hdfs dir >  < local file >
```

* cp

Copy files from source to destination. This command allows multiple sources as well in which case the destination must be a directory.

```
hadoop fs -cp  < hdfs file >  < hdfs file >
```

* mv

Moves files from source to destination.

```
hadoop fs -mv < hdfs file >  < hdfs file >
```

* count

Count the number of directories, files and bytes under the paths that match the specified file pattern.

```
hadoop fs -count < hdfs path >
```

* du

Displays sizes of files and directories contained in the given directory or the length of a file in case its just a file.

```
hadoop fs -du < hdsf path> # every file
hadoop fs -du -s < hdsf path>  #all files sum
hadoop fs -du - h < hdsf path> 
```

* text

Takes a source file and outputs the file in text format. 

```
hadoop fs -text < hdsf file>
```

* setrep

Changes the replication factor of a file. If path is a directory then the command recursively changes the replication factor of all files under the directory tree rooted at path.

```
hadoop fs -setrep -R 3 < hdfs path >
```

* stat

Print statistics about the file/directory at <path> in the specified format. Format accepts filesize in blocks (%b), type (%F), group name of owner (%g), name (%n), block size (%o), replication (%r), user name of owner(%u), and modification date (%y, %Y). %y shows UTC date as “yyyy-MM-dd HH:mm:ss” and %Y shows milliseconds since January 1, 1970 UTC. If the format is not specified, %y is used by default.

```
hdoop fs -stat [format] < hdfs path >
```

* tail

Displays last kilobyte of the file to stdout.

```
hadoop fs -tail < hdfs file >
```

* archive

compress files

```
hadoop archive -archiveName name.har -p < hdfs parent dir > < src >* < hdfs dst >
hadoop fs -ls /des/hadoop.jar
hadoop fs -ls -R har:///des/hadoop.har
```

* balancer

```
hdfs balancer
```

* dfsadmin

```
hdfs dfsadmin -help
hdfs dfsadmin -report
hdfs dfsadmin -safemode < enter | leave | get | wait >
# enter：enter safe mode
# leave：leave safe mode
# get: to know whether to start safe mode
# wait: wait for safe mode
```
