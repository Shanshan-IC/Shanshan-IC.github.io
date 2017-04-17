---
layout:     post
title:      "计算广告学 笔记4.3 流量预测和ZooKeeper"
category:   Ad
tags:   Ad
---

* content
{:toc}

课程地址：[计算广告学](http://study.163.com/note/noteIndex.htm?id=321007&type=0#/noteIndex?resType=0&resId=435072&sortType=0)

## 课时22	流量预测

在前面合约式广告中提到过合约式广告中有三个基本技术，1. 受众定向，2. 点击预测，3. 流量预测。在这三个技术基础上才可以做Online Allocation，本节主要介绍流量预测。

在定向条件分的比较粗的情况下，流量预测是比较简单的，比如只对人群分了几十个类，那么只需要进行简单的统计就可以进行流量预测了。

这里只介绍一种简单的，但很有启发意义的方法。这种方法是将查询视为a，文档集是(u,c)的一个反向检索的过程。与之相对的是在广告检索的过程中，查询是(u,c)，文档集是a。这种方法对u或c进行检索，所检索出的数量也就是流量的大小。之所以要这样做的原因是，广告的定向条件的可能组合非常多，不可能通过简单的统计来完成。

因为(u,c)的联合空间规模过大，无法直接对联合空间进行处理，也没有必要这样。所以需要对u和c分别处理。即分别对受众和页面建索引，用广告进行索引，可以得到满足定向的受众和页面量分别是多少。


## 课时23	ZooKeeper 介绍

举一个使用场景，比如我们有很多台Index，或者有很多台Ad Server，其中有一些机器崩溃了，或是有一些机器新添加进了集群，如何用一个分布式的管理系统通知其它相关模块，哪些机器是可以用的。ZooKeeper就是解这种问题的，ZooKeeper是在基于消息传递通信模型的分布式环境下解决一致性问题的基础服务。

**Paxos算法**

Paxos 算法解决的问题是一个分布式系统如何就某个值（决议）达成一致。一个典型的场景是，在一个分布式数据库系统中，如果各节点的初始状态一致，每个节点执行相同的操作序列，那么他们最后能得到一个一致的状态。为保证每个节点执行相同的命令序列，需要在每一条指令上执行一个“一致性算法”以保证每个节点看到的指令一致。一个通用的一致性算法可以应用在许多场景中，是分布式计算中的重要问题。因此从20世纪80年代起对于一致性算法的研究就没有停止过。节点通信存在两种模型：共享内存（Shared memory）和消息传递（Messages passing）。Paxos 算法就是一种基于消息传递模型的一致性算法。