---
title: java容器-Map和Set
date: 2019-10-15 22:16:18
tags: java
categories: java
---
今天介绍一些java内的容器-Map和Set，有些容器会在后续案例中更详细介绍


### Map
- HashMap
  - 实现map接口， key value键值对
  - 内部实例变量size表示实际键值对的个数。table是一个Entry类型的数组，称为哈希表或哈希桶，其中的每个元素指向一个单向链表，链表中的每个节点表示一个键值对，Entry是一个内部类，其中，key和value分别表示键和值，next指向下一个Entry节点，hash是key的hash值；
  - 扩展策略： threshold表示阈值，当键值对个数size大于等于threshold时考虑进行扩展， 一般而言，threshold等于table.length乘以loadFactor，会分配一个容量为原来两倍的Entry数组，调用transfer方法将原来的键值对移植过来，然后更新内部的table变量，以及threshold的值
  - key比较的时候，是先比较hash值，hash相同的时候，再使用equals方法进行比较，要求元素重写hashCode和equals方法
  - 保存键值对的流程：
    - 计算键哈希值
    - 根据哈希值取得保存位置
    - 插到对应位置的链表头部或更新已有值
    - 根据需要扩展table大小
  - 分配一个容量为原来两倍的Entry数组，调用transfer方法将原来的键值对移植过来，然后更新内部的table变量，以及threshold的值
  - hash值是随即的，键值对没有顺序
- TreeSet
  - 按键有序，TreeMap同样实现了SortedMap和NavigableMap接口，可以方便地根据键的顺序进行查找，如第一个、最后一个、某一范围的键、邻近键等,要求键实现Comparable接口或通过构造方法提供一个Com-parator对象
  - 内部是用红黑树实现的，红黑树是一种大致平衡的排序二叉树
  - 根据键保存、查找、删除的效率比较高，为O(h), h为树的高度，在树平衡的情况下，h为log2(N), N为节点数
- LinkedHashMap
  - 是HashMap的子类，内部还有一个双向链表维护键值对的顺序，每个键值对既位于哈希表中，也位于这个双向链表中。
  - LinkedHashMap支持两种顺序：一种是插入顺序；另外一种是访问顺序； （按访问有序-LRU缓存）


### Set
- hashSet
  - 没有重复元素
  - 可以高效地添加、删除元素、判断元素是否存在，效率都为O(1)
  - 无序
  - 要求元素重写hashCode和equals方法，且对于两个对象，如果equals相同，则hashCode也必须相同
  - 内部是用HashMap实现的
- TreeSet
  - 有序
  - 给予TreeMap实现
  - 添加、删除元素、判断元素是否存在，效率比较高，为O(log2(N)), N为元素个数
  - TreeSet同样实现了SortedSet和NavigatableSet接口，可以方便地根据顺序进行查找和操作，如第一个、最后一个、某一取值范围、某一值的邻近元素等，要求元素实现Comparable接口或通过构造方法提供一个Com-parator对象
- LinkedHashSet
  - 内部的Map的实现类是LinkedHashMap



### 特别说明
- HashMap也不是线程安全的，并发场景下需要注意，可以使用HashTable，但是相应效率地下，可以使用ConcurrentHashMap，兼顾性能和并发
- map的keySet和entrySet返回都是set，所以一般可以用map实现对应的set；
