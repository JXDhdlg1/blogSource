---
title: java基础学习之string专题
date: 2017-03-23 10:07:29
tags: java
categories: java
---
今天介绍下java中的String

### 用法
- 定义String变量
```
String a = "test";
```
- new 创建
```
String b = new String("test");
```
- 可以直接使用+ += 运算

### 内部原理
- String类内部用一个字符数组表示字符串
- String会根据参数新创建一个数组，并复制内容，而不会直接用参数中的字符数组。String中的大部分方法内部也都是操作的这个字符数组

### 不可变性
- String类也是不可变类，即对象一旦创建，就没有办法修改了。String类也声明为了final，不能被继承，内部char数组value也是final的，初始化后就不能再变了
- String类中提供修改的方法，是通过创建新的String对象来实现的，原来的String对象不会被修改

### 常量字符串
- 字符串常量放在字符串常量池
- 直接使用常量的定义引用的是常量池内同一个对象，相等，new 出来的则是新的对象

### 特别说明
- 如果频繁修改字符串，而每次修改都新建一个字符串，那么性能太低，这时，应该考虑Java中的另两个类StringBuilder和StringBuffer
-
