---
title: elasticsearch升级-transportClient转HighLevelRestClient
date: 2019-11-02 06:53:22
tags: elasticsearch
categories: elasticsearch
---
今天分享下项目中进行elasticsearch升级，同时伴随着transport Client转换位High Level Rest Client.

### 升级迁移步骤
- es 集群升级（DBA操作）
- 数据全量迁移
- 使用High Level Rest Client和transport Client对新老集群双写；
- 数据全量迁移
- 读改到升级后新集群
- 老集群断写入

### 架构
- ![架构简介](/images/es_jg.png)


### 注意事项
- 数据迁移过程中双写，并建立补偿机制，避免数据丢失
- 核心业务部署双集群，封装DR
- 建立db数据和es数据的全量同步流程，修复数据不一致
