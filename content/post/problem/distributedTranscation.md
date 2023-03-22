---
title: "记一次分布式事务爬坑"
date: 2023-03-20T21:36:16+08:00
categories:
- spring
- 问题
tags:
- 分布式事务

keywords:
- 分布式事务
- TransactionSynchronizationManager 
- Seata
#thumbnailImage: //example.com/image.jpg
---

在企业生产实践中遇见这样一个和分布式事务相关的问题，在程序运行中事务提交涉及跨rpc调用，如何保证事务提交和rpc调用的结果一致，避免不同系统的数据不一致。
<!--more-->


# 问题的产生

问题已经如前言所述，这里做一个简单的代码展示。

```java
@Transactional(rollBackFor = Exception.class)
public void transFunc() {
	// 方法1
	doSth1();
	
	// 异步远程调用
	asyncRpcCall();

	// 方法2
	doSth2();
}
```

在该事务方法中asyncRpcCall()调用生效后，但本地事务没提交，导致对方系统的数据和本地数据不一致。  
在这里不能简单的认为将asyncRpcCall()移至方法最后，或将其改为同步调用就能解决问题。  
因为，有时同步调用是十分耗时的，如果本地业务处理不依赖于这个调用的话就应该让这里是异步非阻塞的，加快本地业务处理速度。  
其次将方法移至最后也并非是可靠的。因为是异步的，所以即使发起了调用，这里的事务也可能未提交，导致数据不一致。

# 分布式事务介绍

说一千，道一万，这里其实已经涉及到分布式事务的处理了。而且在平时的开发中，这样的需求也是常见的，业界也有成熟的理论去描述这种现象，并提出可落地的解决方案。


## CAP与ACID

CAP定理，在一个分布式系统中，设计共享数据问题时，以下三个特性最多只能同时满足其中两个：  
- 一致性（Consistency）：代表数据在任何时刻、任何分布式节点中所看到的都是符合预期的。一致性在分布式研究中是有严肃定义、有多种细分类型的概念，以后讨论分布式共识算法时，我们还会再提到一致性，那种面向副本复制的一致性与这里面向数据库状态的一致性严格来说并不完全等同，具体差别我们将在后续分布式共识算法中再作探讨。  
- 可用性（Availability）：代表系统不间断地提供服务的能力，理解可用性要先理解与其密切相关两个指标：可靠性（Reliability）和可维护性（Serviceability）。可靠性使用平均无故障时间（Mean Time Between Failure，MTBF）来度量；可维护性使用平均可修复时间（Mean Time To Repair，MTTR）来度量。可用性衡量系统可以正常使用的时间与总时间之比，其表征为：A=MTBF/（MTBF+MTTR），即可用性是由可靠性和可维护性计算得出的比例值，譬如 99.9999%可用，即代表平均年故障修复时间为 32 秒。
- 分区容忍性（Partition Tolerance）：代表分布式环境中部分节点因网络原因而彼此失联后，即与其他节点形成“网络分区”时，系统仍能正确地提供服务的能力。







# 几种可能的解决方案


# 


# 参考文献
- [Spring 事务扩展机制 TransactionSynchronization](https://www.cnblogs.com/kkkfff/p/13778692.html)
- [凤凰架构](http://icyfenix.cn/architect-perspective/general-architecture/transaction/distributed.html)
- [Seata](https://seata.io/zh-cn/)
