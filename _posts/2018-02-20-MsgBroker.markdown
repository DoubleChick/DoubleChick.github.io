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
消息中间件(消息服务)为分布式系统之间提供了一种直接服务调用之外的异步通讯方式.
在这个通讯过程中主要分为三个部分:消息发布者(Publisher)、消息中间件(MsgBroker)、消息订阅者(Subscriber).通过一张来看一下大体的通讯过程~

![img](/img/in-post/MsgBroker1.png)

* 消息发布者(系统或组件)将消息(通常包含业务参数)发布到MsgBroker中
* MsgBroker根据消息类型将消息分别传送给对应的消息订阅者,消息订阅者(系统或组件)根据消息类型与内容产生不同行为
* 消息中心中维护着消息的订阅关系,而使得Publisher与Subscriber互相不感知彼此,降低了系统间的耦合度,从而提高了架构的扩展性

`MsgBroker在此基础上提供了事务型消息的支持、支持集群水平扩展、对Sofa框架提供了良好的集成..等等`

写到这儿的时候,在项目中也接触了一些中间件(Middleware)了.个人感觉中间件就是将一些符合当下需求的(分布式存储、缓存、消息等等)、常用的、成熟的设计模式或架构抽象独立出来,并封装好.
让分布式系统都能更加专注各自的业务上,只需遵循各中间件对框架的集成规则去使用,就可以实现降低系统耦合,提高性能吞吐量等众多好处.

这样来看MsgBroker就是实现了“发布/订阅”模式的功能包,其中大多数原理与其他主流的消息代理组件相似,在这基础上结合蚂蚁生态内业务需要的特殊属性进行改进、并提供了一些具有优势的技术特性!

## Sofa中的使用方式

```xml
<sofa:consumer id="subscriber" group="S_appname_service">
	<sofa:listener ref="uniformEventMessageListener" />
	<sofa:channels>
		<sofa:channel value="topicName">
			<!-- 消息1 -->
			<sofa:event eventCode="eventCode1" waterMark="-1" persistence="false" />
			<!-- 消息2 -->
			<sofa:event eventCode="eventCode2" waterMark="-1" persistence="true" />
		</sofa:channel>
	</sofa:channels>
	<sofa:binding.msg_broker />
</sofa:consumer>
```
MsgBroker中的消息类型由Topic(代码中的topicName)和EventCode共同标识,Topic代表一个消息大类(如TP_F_SC定时任务),EventCode标识消息大类下的一个消息子类
一般消息大类Topic的新增变更较少,新增消息类型更多的是新增消息子类EventCode.


## 持久订阅&非持久订阅








