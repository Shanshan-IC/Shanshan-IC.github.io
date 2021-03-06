---
layout:     post
title:      "计算广告学 笔记3.1 受众定向"
category:   Ad
tags:		Ad
---

* content
{:toc}

课程地址：[计算广告学](http://study.163.com/note/noteIndex.htm?id=321007&type=0#/noteIndex?resType=0&resId=435072&sortType=0)

## 课时14 受众定向的概念

受众定向是指按人群来划分对广告的售卖和优化，它是在线广告中最核心的部分。受众定向是在线广告区别于线下广告最本质的部分。

受众定向是为ROI优化中打标签的过程，它是对Ad，User，Context打标签。受众定向中有一种特殊的定向，上下文标签，即通过用户所浏览的网页，判断用户的兴趣。这种定向一般认为是上下文定向，但个人认为上下文标签也可以认为是用户即时的兴趣或是标签。

标签有两大主要作用：1. 建立面向广告主的流量售卖体系，这一点本身就决定了标签不能按系统优化的思路来设计，即所打的标签一定要能被广告主理解。比如对上下文打标签，要对页面进行分类，个人认为更有效的方式是对页面进行supervise learning，即预先定义好标签体系，然后对页面进行分类，而不应该直接用聚类的方法或是Topic Model的方法打出一些无法直接解释的标签，因为无法对广告主进行售卖。这点是广告与其它用户产品不同的地方。2. 为各机器学习模块（如CTR预测）提供原始特征，比如提供性别，年龄等特征供机器学习分析。

举一个例子来说明什么是一个标签体系，广告有三个轴，User，Ad，Context。

![](/images/images/ad/19.jpg)

受众定向方式，我们基本可以分为三类。1. 对user提feature，2. 对context提feature，为什么要将这两类分开，我前面讲对可以将context看成是即时受众标签，但因为它们系统上的解决方案是不一样的，所以将它们分开。3. 对Ad和User的组合打标签，即在特定的广告主条件下，用户应该打什么标签，这种标签就引出了我们后面要讲的Demand方的Audience Segmentation，即根据广告主的逻辑给用户打标签。

![](/images/images/ad/20.jpg)

我们逐个看一下图中的定向方法。我们从效果最好的看起，效果最好的是重定向，它是公认的对direct response最好的一种方式，这种方式就是f(a,u)，即demand-side的定向方式，它做的事很简单，如果一个用户访问过广告主的网站，就给用户打上某一种标签。2.2明确揭示推荐的原因，比如我是京东用户，我看到京东的广告，我非常清楚为什么这个广告会推给我。2.3 符合用户的意义，这点也是满足的，因为我访问过这个网站，3.1 广告是在用户的理解范围，这点当然也是满足的。国内做重定向的公司很多，比如淘宝的站外广告就很多。重定向从最早产生的motivation上个人认为是有两个层次，第一个层次是做品牌广告，品牌广告就是前面举的例子，我曾经去过一个网站，如果这个网站品牌再由有价值的媒体推送给我，我会感觉自己的决策是正确的，并会对这个网站品牌更有信心。另一层次是效果广告，比如我现在要买一个电视机，我在京东上是处在浏览阶段，或是加入购物车，或是已经下单，它会针对用户所处的阶段，会做非常细分的促销策略，比如用户在浏览阶段，那所投的广告最好是让用户能转化到加入购物车，比如发给用户一些热销或是促销的商品。如果用户已经加入购物车，广告最应该是促进用户下单的。如果用户已经付款了，广告应该将他所购买的相似产品推荐给他。淘宝的Retargeting技术个人感觉还是有些单一，比如你去淘宝某一网店买过玩具，它就会一直推荐玩具品类的广告，但效果也是不错的，然而仍有深挖的空间。

地域和人口属性概念很好理解，它是Ad Serving和合约式广告系统就产生了的定向方式，为了把流量粗分一下，把流量卖出更高的价格，这种定向方式是很粗浅的，人口基本就是性别，年龄等几种不多的类别（注：在社交广告中人口属性会多一些，比如腾讯广告，它掌握比较多的人口信息），人口属性定向成为必备的定向方式是因为这是广告主所熟悉的语言，在线下广告就用的是这种方式，所以用这种方式是最容易被广告主接受的方式。地域基本就是按IP地址分地区。

我们重点探讨上下文和行为，上下文是对context打标签的行为，它的原理：2.1 不要打断或干扰用户的任务，这是上下文之所以成立的一个原理性的原因，3.1 广告是在用户的理解范围之内，比如用户所看的财经网页，广告是E-Trade，用户肯定是有兴趣，也是能理解的，它的效果如果做的好，是比人口属性和地域定向方式要好，但它远远不能与重定向相比。行为定向是根据用户的历史行为进行推荐，比如用户浏览过哪些网页，搜索过哪些关键字，甚至用户线下的一些线下行为。中国的广告线下行为应用的不多，但美国广告线下行为使用的很多。它的效果与上下文总体来讲差不多。网站/频道这种定向非常简单，比如女性，军事频道。它对某些特定的频道效果还可以，比如汽车频道，汽车广告的效果会好很多。

Hyper-local对应对地域定向，传统所说的地域定向一般是到城市级别或到省的级别，但这种定向效果一般，Hyper-local是把地域定向做到非常细的粒度，比如定向清华园的主楼附近，这种定向会产生非常多的新的广告的需求，比如一个咖啡店就可以定向它附近的人群，而不使用这种定向，类似咖啡店，小饭馆的广告主无法投门户广告和搜索引擎广告，它唯一的选择是在路边发广告。

Look-alike是Demand side的定向方式，刚才提到重定向的效果是非常好的，但是它的数据量非常小，并且数据量不由广告平台决定，是由广告主的网站决定的。一些线上业务不是很强，但又有reach它用户的需求的广告主，比如银行和汽车网站，网站流量不大，也可以对它们做retargeting，但是量太小，没什么价值。所以它们希望达到的是广告平台通过海量数据，找到与广告主网站用户相似的人群。比如：银行可以提供一万个信用卡用户，然后广告平台用一万个信用卡用户信息来找到十万个可能对该银行信用卡感兴趣的人群。这种方式可以认为是重定向的扩量的行为，一般来讲，在同样量的基础上，它要比与demand side无关的方式要好。

概括地讲，定向方式的趋势是：先是线下对一些对人口分类的一些逻辑，先移到了线上，逐渐产生了上下文定向，行为定向，网站/频道定向等一些定向方式，这些方式都可以称为Supply side定向方式，最后产生的是Demand side定向方式，有重定向和Look-alike定向方式。

Audience Science公司是比较早提出Audience Targeting的概念的，它的核心业务是：1 主要提供面向publish的数据加工服务。比如它的一个大客户NewYork Times，NewYork Times自己有很多用户，也有很多在线数据，但很显然它的核心业务不是做广告，也不是做数据加工，它更愿意把数据交给Audience science，Audience science帮它加工一些有意义的用户标签，比如财经类用户，体育类用户。NewYork Times的BI可以用这些标签，分析哪些用户对哪些内容感兴趣，应该如何优化内容。2. Audience Science还直接运营ad network，并帮助广告主进行campaign管理和优化，这里它就用到了它分析得到的标签。

Audience Science数据标签不像bluekai那样在市场上公开出售，仅供委托他们优化compaign的广告商使用，即它的标签只为它自己的network服务。使用标签impression创造的营收执照一定比例跟publisher分成。

具体的工作流程是：publisher先把自己的流量托管给audience science，并给Audience Science一定的技术服务费，Audience Science把数据加工成标签，首先提供给publisher用，publisher用标签优化它的流量和BI。同时它在自己的Ad Network中对这些数据进行变现，变现的数据过来又可能与publish分成。


