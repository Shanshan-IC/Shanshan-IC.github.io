---
layout:     post
title:      "计算广告学 笔记6 广告交易市场"
category:   Ad
tags:		Ad
---

* content
{:toc}

课程地址：[计算广告学](http://study.163.com/note/noteIndex.htm?id=321007&type=0#/noteIndex?resType=0&resId=435072&sortType=0)

## 课时31 广告交易市场

广告交易平台：

关键特征：用实时竞价（RTB）方式链接广告和（上文，用户）；按照展示上的竞价收取广告主费用

## 课时32 实时竞价

* 实时竞价 Real time bidding(RTB)
	RTB 的流程可以分为cookie mapping 和Ad 

* call两个过程
	cookie mapping的作用是沟通Adx和DSP，使得两边都了解有哪些cookie
	ad call是正式的广告投放

这里面有一些潜在的风险，如有些公司加入RTB目标就是用非常廉价的方式拿到用户数据，而非投广告。并且，由于多了一次访问请求返回，会增加浏览者的网页响应时间。对于用户来说，等待大约多了 100ms，这样对用户 ctr 是有影响的，并且增加了Demand端的成本和server的成本

## 课时33 Cookie Mapping
 
第一个例子：DSP和adExchange 之间进行Cookie Mapping，由DSP发起，在广告主控制的网站上发起，mapping表存在DSP端，目的是为了获取DSP cookie和Adx cookie之间的对应关系。
当用户浏览含有DSP代码的网页的时候，网页向DSP提出询问请求，
DSP cookie服务确认该网页用户的cookie很久没有更新过了，就向该页面提出我需要同步你的cookie
然后该页面将相关信息提交给ad exchange,xid= adx cookie id(这个不明白，dsp端是怎么获得的，是否xid是代表exchange的ID)，did（demand cookie id），dck = demand cookie 
adx把对应的xck= adx cookie返回给DSP端
到此为止，DSP端就把自己的cookie和ADX端的cookie对应起来了，存在DSP端的表里面。

当以后广告需求产生的时候，ADX把xck发给DSP，DSP在自己的表里查，这个人是不是我要的，是要的，我再出价购买。

第二个例子：

网站想了解访问自己网站用户的更多消息，或者用户的分类，标签等等，所以需要向dmp询问
网站自己存自己的用户cookie和dmp cookie的映射
如果网站想了解用户，就先查表，获得dmp cookie，然后向dmp发送这个用户的dmp cookie，dmp就返回这个用户标签等等

课时34 Supply Side Platform

对于媒体，有四种变现模式：

* 大媒体，直接GD销售，变现能力最高（按天销售）

* 分类流量后，按照GD销售（按CPM销售，target）

* 流量托管给广告联盟

* RTB

SSP等于是同时做这4个，收益统一管理，灵活接入多种变现方式。Sell-Side Platform，即供应方平台。供应方平台能够让网络媒体也介入广告交易，从而使它们的库存广告可用。通过这一平台，网络媒体希望他们的库存广告可以获得最高的有效每千次展示费用，而不必以低价销售出去。

## 课时35 Demand Side Platform

需求方平台 Demand Side Platform：需求方平台允许广告客户和广告机构更方便地访问，以及更有效地购买广告库存，因为该平台汇集了各种广告交易平台的库存。

目的：Allows digital advertisers to manage multiple ad exchange and data exchange accounts through one interface

关键特征：

定制化用户划分

跨媒体流量采购

通过ROI估计来支持RTB

代表：InviteMedia， MediaMath

## 课时36 DSP流量预测
 
开放的问题：如何利用历史投放数据估计流量？（没有公认的合适的方法）

## 课时37 DSP点击价值估计

点击价格估计的应用场景：

* DSP的实时出价

* 广告网络的出价工具

* 智能定价：广告网络方需要对不同质量的流量估计一个相对的价值，方便对广告主打折（比如说上下文的5折，搜索引擎的全价）。

这个问题作为机器学习的挑战：

* 数据非常稀疏

* 与广告主类型强烈相关的行为模式
点击价值估计若干原则

模型估计时，用较大的bias换较小的variance，已达到稳健估计的目的

充分利用广告商类型的层级结构，以及转化流程上的特征

## 课时38 DSP重定向

DSP：DSP大致有3个功能，重定向、人群标签、相似用户。	

重定向的分类：

1、网站重定向：根据浏览的网站的内容进行重定向。对做品牌的够用了。比如进入过京东商城，到别的网站去给你推荐京东的东西。

2、搜索重定向： 根据搜索行为

3、个性化重定向： 

根据浏览、关注、购买等各阶段，进行适合的推荐。
个性化重定向：粒度是商品。没下单，激励下单，已下单，推荐相关。

和推荐不同的是，推荐是按照上下文推荐，比如说前一个页看到，而这个主要是给user打标签

推荐算法概述：

1、协同过滤：

2、基于内容方法

3、推荐算法的本质？ 对{user、a}的co-occurence这一稀疏矩阵的参数或非参数化的描述。

4、推荐算法选择的关键：探索较合适的bias和variance的平衡，以适应问题的数据稀疏性

## 课时39 需求端推荐方法

## 课时40 广告流量交易方式

广告交易市场中的问题还没有形成系统的体系，所以主要介绍概念，算法和技术还不成定论。

广告流量交易方式

1.程序交易（programmatic trade）
实时竞价（RTBS RTBD）、Adx、优选、网络优化、组合优化、ad network

2.优先销售（premium sale）
CPT、Guaranteed Delivery担保投送、Ad server
趋势是市场向demand方向发展，并且越来越侧重于程序购买
