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
- Subject：是一种桥接或代理，在 ReactiveX 的某些实现中可用，它既充当观察者，也充当可观察。
- Scheduler：调度，如果要在多个Operators中运用多线程，可以通过指定某些Operators或特定的Observable在特定的Scheduler上进行操作来实现。

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

## 实例

#### 单击按钮事件流

![button_click](https://snlo.app/img/blog_img/191029/button_click.jpg)

点击事件数据流是按时间顺序排列的一系列进行中的事件，它可以发出三种不同的事件，一个新值来自流的**next**事件，一个**error**事件，一个**complete**事件。例如，在包含该流的当前视图关闭时，会发出complete。

通过定义在将发next时执行的函数，在发出error时的另一个函数以及发出complete时的另一个函数，来异步捕获这些发出的事件，有时候可以忽略最后两个，而只专注于为next事件定义的函数。对流的这种监听被定义为订阅（**subscribe**），定义的函数式观察者（**observer**），流是正在被观察的（**observable**），这也符合观察者设计模式。

以上就是单击按钮事件流的函数响应式编程的思路，在不同框架下各自的实现如下：

- ReactiveObjC

  ```swift
  [[self.buttonTest rac_signalForControlEvents:UIControlEventTouchUpInside] subscribeNext:^(__kindof UIControl * _Nullable x) {
      NSLog(@"点击事件：%@",x);
  } error:^(NSError * _Nullable error) {
      NSLog(@"错误：%@",error);
  } completed:^{
      NSLog(@"完成");
  }];
  ```

- ReactiveCocoa - ReactiveSwift

  ```swift
  self.buttonTest.reactive.controlEvents(.touchUpInside).observe { (event) in
      switch event {
      case .value(let sender):
          print("点击：\(sender)")
      case .failed(let error):
          print("错误：\(error)")
      case .completed:
          print("完成")
      case .interrupted:
          print("中断")
      }
  }
  ```

- RxCocoa - RxSwift

  ```swift
  let disposeBag = DisposeBag()
  self.buttonTest.rx.controlEvent(.touchUpInside).subscribe(onNext: { (_) in
      print("点击")
  }, onError: { (error: Error) in
      print("错误：\(error)")
  }, onCompleted: {
      print("完成")
  }, onDisposed: {
      print("处理掉了")
  }).disposed(by: disposeBag)
  ```

几种实现虽然有所不同，但它们的思路是一致的。

#### 双击按钮事件流

当前点击事件的发生与上一次点击事件的发生的时间间隔假如为250ms，我们就定义为双击。在响应式编程中，我们需要创建从原始点击事件流转换或者过滤而来的新的双击事件流，然后再订阅它。

这个双击事件流表示一个按钮被连续（自定义250ms时间间隔）点击了两次的事件，怎么得到这个流呢？常见的Reactive库中，每个Stream都附加了许多的Functional，比如：map、filter、scan等等，当调用某个函数时，会在原来的Stream的基础上返回一个新的Stream，并且它不会以任何的方式修改原始的Stream，在Reactive这似乎就是一个不变的特性。

![map_scan](https://snlo.app/img/blog_img/191029/map_scan.jpg)

如上图，该`map(c = 1)`函数将替换每个发送值为‘1‘再映射到新的Stream。该`scan( += 1)`将Stream上的所有之前的值叠加产生新的Stream，再订阅它，当发生点击时响应当前总的点击次数。

命令式编程就复杂多了，响应双击事件，需要保存状态的一些变量和计算时间间隔代码等一大堆的代码。在响应式编程中这就变得简单而清晰多了，下图为响应双击时间流的分析：

![double_click](https://snlo.app/img/blog_img/191029/double_click.png)

实际上只需要4步就可以完成响应，首先通过`buffer(time:250ms, scheduler)`函数把连续250ms内的点击都累积到一个列表中，得到一个列表的stream，然后用`map(list.count)`函数把每个列表映射为一个列表长度的整数，然后再使用`filter(count == 2)`过滤出整数为2的数据，得到最终想要的stream，最后再订阅这个stream。能感受到它的清晰简单吗？下面是代码实现：

- ReactiveObjC：

```swift
[[[[[self.buttonTest rac_signalForControlEvents:UIControlEventTouchUpInside]
    bufferWithTime:0.250 onScheduler:scheduler] map:^id _Nullable(RACTuple * _Nullable value) {
    NSLog(@"映射：%@",value);
    return @(value.count);
}] filter:^BOOL(id  _Nullable value) {
    NSLog(@"过滤：%@",value);
    return [value integerValue] == 2;
}] subscribeNext:^(id  _Nullable x) {
    NSLog(@"双击结果：%@",x);
} error:^(NSError * _Nullable error) {
    NSLog(@"错误：%@",error);
} completed:^{
    NSLog(@"完成");
}];
```
- ReactiveCocoa - ReactiveSwift：


```swift
self.buttonTest.reactive.controlEvents(.touchUpInside)
    .collect(every: DispatchTimeInterval.milliseconds(250), on: QueueScheduler.main, skipEmpty: true, discardWhenCompleted: true)
    .map{ $0.count }
    .filter{ $0 == 2 }
    .observeResult { (resulet) in
        print("双击：\(resulet)")
}
```
- RxCocoa - RxSwift：


```swift
self.buttonTest.rx
    .controlEvent(.touchUpInside).asObservable()
    .buffer(timeSpan: RxTimeInterval.milliseconds(250), count: 0, scheduler: MainScheduler.init())
    .map{ $0.count }
    .filter{ $0 == 2 }
    .bind { (_) in
        print("双击")
}.disposed(by: disposeBag)
```



## 参考

<a href= "https://gist.github.com/staltz/868e7e9bc2a7b8c1f754" target="_blank">《The introduction to Reactive Programming you've been missing》</a>