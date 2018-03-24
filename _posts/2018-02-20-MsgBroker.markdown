---
layout:     post
title:      "消息中间件 MsgBroker"
subtitle:   ""
date:       2018-02-20 13:30:00
author:     "ZJF"
header-img: "img/post-bg-unix-linux.jpg"
catalog: false
tags:
    - 蚂蚁中间件
---
## 消息服务基础概念
	消息中间件(消息服务)为分布式系统之间提供了一种直接服务调用之外的异步通讯方式
	在这个通讯过程中主要分为三个部分:消息发布者(Publisher)、消息中间件(MsgBroker)、消息订阅者(Subscriber).通过一张来看一下大体的通讯过程
![img](/img/in-post/MsgBroker1.png)
* 消息发布者(系统或组件)将消息(通常包含业务参数)发布到MsgBroker中
* MsgBroker根据消息类型将消息分别传送给对应的消息订阅者,消息订阅者(系统或组件)根据消息类型与内容产生不同行为
消息中心中维护着消息的订阅关系,而使得Publisher与Subscriber互相不感知彼此,降低了系统间的耦合度,从而提高了架构的扩展性

MsgBroker在此基础上提供了事务型消息的支持、支持集群水平扩展、对Sofa框架提供了良好的集成..等等


## 持久订阅&非持久订阅








