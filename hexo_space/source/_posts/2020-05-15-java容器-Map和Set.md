---
title: java容器-Map和Set
date: 2020-05-15 22:16:18
tags: java
categories: java
---
今天介绍一些java内的容器-Map和Set，有些容器会在后续案例中更详细介绍


### Map
- HashMap
  - 实现map接口， key value键值对
  - 内部实例变量size表示实际键值对的个数。table是一个Entry类型的数组，称为哈希表或哈希桶，其中的每个元素指向一个单向链表，链表中的每个节点表示一个键值对，Entry是一个内部类，其中，key和value分别表示键和值，next指向下一个Entry节点，hash是key的hash值；
  - 扩展策略： threshold表示阈值，当键值对个数size大于等于threshold时考虑进行扩展， 一般而言，threshold等于table.length乘以loadFactor，会分配一个容量为原来两倍的Entry数组，调用transfer方法将原来的键值对移植过来，然后更新内部的table变量，以及threshold的值
  - key比较的时候，是先比较hash值，hash相同的时候，再使用equals方法进行比较
  - 保存键值对的流程：
    - 计算键哈希值
    - 根据哈希值取得保存位置
    - 插到对应位置的链表头部或更新已有值
    - 根据需要扩展table大小
  - 分配一个容量为原来两倍的Entry数组，调用transfer方法将原来的键值对移植过来，然后更新内部的table变量，以及threshold的值
  - hash值是随即的，键值对没有顺序
  

### Set

### 特别说明
- HashMap也不是线程安全的，并发场景下需要注意，可以使用HashTable，但是相应效率地下，可以使用ConcurrentHashMap，兼顾性能和并发
