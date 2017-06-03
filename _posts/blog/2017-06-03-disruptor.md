---
layout: post
title: Disruptor
categories: Java
description:  Disruptor高性能生产消费队列实现
keywords: Disruptor
---

最近在部门内部做了一次关于Disruptor的分享。<!--\n\n-->

## 1. What-Disruptor简介
抽象点：
A High Performance Inter-Thread Messaging Library。
（Disruptor是Java实现的用于线程间通信的消息组件。）  
具体点：
Disruptor是一种可替换有界队列的、高性能的异步处理框架，或者可以认为是最快的消息框架(轻量的JMS)，也可以认为是一个观察者模式实现，或者事件-监听模式的实现，直接称disruptor模式。

项目主页:[https://github.com/LMAX-Exchange/disruptor](https://github.com/LMAX-Exchange/disruptor)  
测试报告:[https://github.com/LMAX-Exchange/disruptor/wiki/Performance-Results](https://github.com/LMAX-Exchange/disruptor/wiki/Performance-Results)

## 2. Where-应用场景
目前，包括Apache Storm、Camel、Log4j 2在内的很多知名项目都应用了Disruptor以获取高性能。

它适合异步队列生产消费场景，在并发线程间交换数据的有界队列的高性能替代
* 在一些获取验证码，发短信的场景下
* 对于一些奖品，卡券的发放，在高峰期，可以只入队，在之后用异步的方式慢慢发放
* 对于比较复杂的逻辑可以进行并发操作
* 使用任务队列将一些不需要与主线程同步执行的任务扔到任务队列异步处理即可

## 3. Why-特点

* 无锁的RingBuffer队列设计
* 避免伪共享
* 采用CAS,减少共享资源的并发互斥
* 使用内存屏障保证可见性

特性详情请参考美团的解析博文：[http://tech.meituan.com/disruptor.html](http://tech.meituan.com/disruptor.html)

## 4. Why-组件

![Disruptor组件图](https://github.com/LMAX-Exchange/disruptor/wiki/images/Models.png)

组件详细介绍：[https://github.com/LMAX-Exchange/disruptor/wiki/Introduction](https://github.com/LMAX-Exchange/disruptor/wiki/Introduction)

## 5. How-技术能怎么玩

![1P-1C](https://camo.githubusercontent.com/42818e6858cbe3ff2640c9807d3b1e043caee753/687474703a2f2f6c6d61782d65786368616e67652e6769746875622e636f6d2f646973727570746f722f696d616765732f317031632d756e69636173742e706e67)

还有很多,具体请点击下面使用链接：

基本使用：[https://github.com/LMAX-Exchange/disruptor/wiki/Getting-Started](https://github.com/LMAX-Exchange/disruptor/wiki/Getting-Started)  
DSL风格使用方式: [https://github.com/LMAX-Exchange/disruptor/wiki/Disruptor-Wizard](https://github.com/LMAX-Exchange/disruptor/wiki/Disruptor-Wizard)  
2.X使用方式：[https://github.com/LMAX-Exchange/disruptor/wiki/Code-Example-Disruptor2x](https://github.com/LMAX-Exchange/disruptor/wiki/Code-Example-Disruptor2x)  

## 6. How-别人怎么玩的

LMAX:     [http://zkread.com/article/617421.html](http://zkread.com/article/617421.html)  
Canal:    [http://blog.csdn.net/u013256816/article/details/52475190](http://blog.csdn.net/u013256816/article/details/52475190)  
Jstorm:   RPC 采用netty + disruptor保证发送速度和接受速度是匹配的  
张开涛,<<亿级流量 网站架构核心技术>>: ![Redis+Disruptor任务队列](/images/posts/java/disruptor.jpg)

## 7. 我们怎么玩的

采用db+Quartz+Disruptor 做任务调度,实现起来比较简单,就不展现了。


## 8. 整体来说,是一个高性能的队列,快速实现生产消费模式。





