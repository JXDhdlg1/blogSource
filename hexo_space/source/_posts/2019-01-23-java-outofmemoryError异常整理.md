---
title: java-outofmemoryError异常整理
date: 2018-04-23 10:05:28
tags: [java]
categories: java
---
今天介绍java中的一些outofmemoryError

### 介绍

- java虚拟机栈
  - StackOverflowError：如果线程请求的栈深度大于虚拟机所允许的深度
  - OutOfMemoryError：当栈扩展时无法申请到足够的内存

- 本地方法栈
  - StackOverflowError
  - OutOfMemoryError

- java堆
  - OutOfMemoryError

- 方法区
  - OutOfMemoryError

- 运动时常量池
  - OutOfMemoryError

- 直接内存
  - OutOfMemoryError
