---
layout:              post
title:               "函数响应式编程参考"
subtitle:            " \"Functional Reactive Programming (FRP) 指南\""
description:	     "用函数式编程的构建模块进行响应式编程在实际编程过程中的参考指南"
date:                2019-10-02 00:00:00 +0800
author:              "SNLO"
header-img:          "img/header_code.jpg"
catalog:             true
tags:
- FRP
---

> 流行的函数响应式编程（以下简称FRP）程框架有 ReactiveObjc、ReactiveSwift、RxSwift、RxJava、、
>
> 参考将从实例着手

# 概述

<a href= "http://reactivex.io/intro.html" target="_blank">ReactiveX</a>：是<a href= "https://docs.microsoft.com/en-us/previous-versions/dotnet/reactive-extensions/hh242985(v=vs.103)" target="_blank">Reactive Extensions</a>的缩写，一般写为Rx，最初是LINQ的一个扩展，由微软的架构师Erik Meijer领导的团队开发，在2012年11月开源。

- Observable：可观察的对象，简单理解为观察者模式。
- Operators：不同的语言实现都各自实现了一组运算符，有重叠的也有独特的。
- Single：类似于Observable，但总是只发出一个值或错误的通知，而不会发出一系列值。
- Subject：一种桥接或代理
- Scheduler：

<a href= "https://github.com/ReactiveCocoa/ReactiveObjC" target="_blank">ReactiveObjc</a>：受Rx启发的Objective-C框架，后更名为ReactiveCocoa（RAC）。

- Streams：数据流，由RACStream类表示，一个NSObject对象。
- Signals：信号，推驱动流，由RACSignal类表示。
- Subscription：一个订阅者是来自任何正在等待或能够等待的事件信号，在RAC中，订阅者被表示为符合RACSubscriber协议的任何对象。
- Subjects：由RACSubject类表示，一个可以被控制的信号。
- Commands：由RACCommand类表示，当产生交互时，创建并预订阅信号来响应交互可以使执行副作用更容易。
- Connections：由RACMulticastConnection类表示，任意数量的共享订阅者之间的一个订阅。
- Sequences：由RACSequences类表示，拉驱动流，是一种集合，达到类似NSArray的目的。
- Disposables：由RACDisposable类表示，用于取消订阅和清理资源。
- Schedulers：调度，由RACScheduler类表示，是信号执行或结果传递一个串行队列，与NSOperationQueue相似。
- Value types：RAC提供其它的一些类来方便表示流中数据值。RACTuple（元组）、RACUnit、RACEvent。

<a href= "http://reactivecocoa.io/reactiveswift/docs/latest/index.html" target="_blank">ReactiveSwift</a>：是ReactiveObjc的Swift实现，专为Swift设计的。

- Signal：事件的单向流。
- Event：事件流的基本传输单位。
- SignalProduver：创建价值流的延期工作。
- Property：一个始终包含值的可观察框。
- Action：具有预设操作的序列化工作程序。
- Lifetime：限制观察范围。

<a href= "https://github.com/ReactiveX/RxSwift" target="_blank">RxSwift</a>：ReactiveX社区成员，是Rx的Swift实现。

## 原理

**响应式编程是使用异步数据流进行编程**。实际上这很常见，事件总线或典型的点击事件本身就是异步事件流（Event Stream），你可以在该事件流上监听并作出响应（产生副作用）。任何数据值，比如变量、用户输入、属性、缓存、数据结构等都可以创建数据流（Data Stream），你可以监听这些数据流并作出响应。

重要的是可以用函数去创建、组合、过滤等来处理这些Data Stream，这就是**函数式响应式编程**。Stream也可以作为另一个Stream的输入，甚至多个Stream也可以作为另一个Stream的输入。你可以合并两个Stream，可以过滤Stream以获得只包含你感兴趣的事情的Stream，你也可以将数据值从一个Stream映射到另一个Stream。

#### 操作



## 方法、流程、模式



## 实施、工具、经验

## 参考

<a href= "https://gist.github.com/staltz/868e7e9bc2a7b8c1f754" target="_blank">《The introduction to Reactive Programming you've been missing》</a>