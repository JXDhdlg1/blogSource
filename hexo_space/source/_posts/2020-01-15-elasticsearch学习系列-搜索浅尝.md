---
title: elasticsearch学习系列-搜索浅尝
date: 2020-01-15 22:47:30
tags: [elasticsearch, 分布式搜索]
categories: elasticsearch
---
本文简单介绍ES搜索的一些简单尝试

#### 检索文档
```
GET /_index/_type/_id
```
根据库、类型、id搜索数据

#### 简单搜索
```
GET /_index/_type/_search
```
搜索索引_index内类型_type内的所有数据，默认返回10条

#### 查询表达式搜索
```
GET /_index/_type/_search
{
    "query" : {
        "match" : {
            "name" : "Smith"
        }
    }
}
```
搜索name=Smith的数据

#### 复杂搜索
```
GET /_index/_type/_search
{
    "query" : {
        "bool": {
            "must": {
                "match" : {
                    "name" : "smith"
                }
            },
            "filter": {
                "range" : {
                    "age" : { "gt" : 30 }
                }
            }
        }
    }
}
```
查找name=Smith，age大于30的数据

#### 全文搜索
```
GET /_index/_type/_search
{
    "query" : {
        "match" : {
            "about" : "abc def"
        }
    }
}
```
搜索数据包含 abc def，或abd 、 def的数据

#### 短语搜索
```
GET /_index/_type/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "abc def"
        }
    }
}
```
搜索数据包含 abc def的数据，不可拆分
