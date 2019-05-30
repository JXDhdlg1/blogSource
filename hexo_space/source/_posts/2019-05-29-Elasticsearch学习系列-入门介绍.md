---
title: Elasticsearch学习系列-入门介绍
date: 2019-05-29 09:55:42
tags: [elasticsearch, 分布式搜索]
categories: elasticsearch
---
elasticsearch是功能强大的基于Lucene实现的开源搜索引擎。
本文主要从以下个方面对其进行入门介绍。
[推荐文档](https://es.xiaoleilu.com/010_Intro/05_What_is_it.html)

#### 使用场景和优势
- 当我们的数据量非常大的时候，我们会考虑进行分库分表，但是分库分表需要考虑依赖拆分的字段，在某些场景下会很复杂。这时候es的优势可以体现出来：
支持PB级数据的高效存取；
- 当我们的业务数据结构很复杂，表之间的关联关系在关系型数据库中表达困难，表之间的关联错综复杂，我们可以考虑es：他可以以json形式存储结构化和非结构化的数据；
- 此外他还是实时文件存储，支持实时分析搜索；

#### 如何使用
- elasticsearch的使用非常简单。在本地可以很轻松的搭建起来。下面列出简单的步骤（如windows本地）
  - [下载地址](https://www.elastic.co/cn/downloads/elasticsearch)下载对应的包，如windows下的biz包
  - 下载后解压出来，点击es/bin/下的elasticsearch.bat（linux下执行bin/elasticsearch，可[参考](https://juejin.im/post/58d1d7530ce4630057e6053a#heading-2)）
  - 打开本地：http://localhost:9200/ 看到正确的json，即安装运行成功
- 向es内存取数据（具体的字段说明下一节说明）
  - ![post保存数据](/images/post.png)
  - ![get查询数据](/images/get.png)

#### 基本概念说明
- elasticsearch提供了非常好用的restful api操作数据，如上节我们看到的get post，还有put delete等简单操作；
- 这里需要对elasticsearch的一些基本概念介绍下：
  - index：索引，是elasticsearch存储数据的逻辑区域，类似关系型数据库中的database；
  - document：文档，elasticsearch用json标示一个对象，类似关系型数据库中的一行数据；
  - type：类型，文档归属一种type，类似关系型数据库中的table；
  - field：字段，类似关系型数据库中的字段；
- 在es中可以按照以上概念对数据进行组织，存储，查询，聚合等操作；

#### 更多特性和优势
- DSL查询： elasticsearch提供了功能十分强大的DSL查询，用于复杂的场景，可以看文档了解这块，基本上可以满足业务的各种要求；
- 分布式集群：非常便于扩展，支持大量级的数据存储查询；
- 还有排序，搜索...等更多更复杂的特性我们会在后续的使用以及专题中进行更详细的介绍。
