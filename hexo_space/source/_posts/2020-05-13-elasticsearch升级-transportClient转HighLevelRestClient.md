---
title: elasticsearch升级-transportClient转HighLevelRestClient
date: 2020-05-13 06:53:22
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

### 架构转变
- 业务集群
- pub log集群

### 注意事项
- 数据迁移过程中双写，并建立补偿机制，避免数据丢失
- 
