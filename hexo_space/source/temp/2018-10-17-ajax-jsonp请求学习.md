---
title: ajax-jsonp请求学习
date: 2016-01-17 15:33:53
tags: [问题记录]
categories: 问题记录
---

### 问题
在ajax请求jsonp获取跨域接口数据的时候，发现以下两个问题

1. 在chrome的调试处发现js报错提示：success_jsonpCallback function not found
2. 接口返回json数据为a，console.log显示结果为b
 当时的ajax请求代码如下：
```$xslt
$.ajax({
           url:"****",
           data:{},
           dataType :"jsonp",
           jsonp:"callback",
           jsonpCallback:"success_jsonpCallback",
           type:"POST",
           success:function(res) {
             console.log(res)
           }
```
后端接口返回数据如下：
```$xslt
echo "success_jsonpCallback" ."(".jsonData.")";
```
当时是在页面加载的时候就请求获取数据(一共有两个请求-这也是问题的关键所在)
### 解决过程
#### 尝试一
- 因为页面还有点击按钮时候做ajax-jsonp请求，是正常的，所以仔细对比了请求的代码，未发现差异，返回的数据格式进行对比也正常；
- 然后发现出问题的ajax请求返回数据较长，然后调试换上一样的返回，问题依然存在。
#### 尝试二
- 在网上查阅大量资料后，发现也曾遇到这个问题，没有能解决我遇到的问题；
- 尝试给请求做同步请求，问题依然存在
```$xslt
async:false,

```
#### 尝试三
- 将页面其中一个ajax请求注释，刷新页面，问题解决。
### 总结
- 整理了代码，继续查阅了一些资料，总结问题如下：页面加载时发起两次ajax请求，但是定义的callback方法是一样的，这样导致异常。
- 我遇到问题的解决方法有两种
   1. 将两次请求数据放到一个接口返回，只做一次ajax请求
   2. ajax请求不规定回调方法名，生成随机回调方法名，可以解决此问题（更优）
- 修改后代码如下：
ajax请求：
```$xslt
$.ajax({
      url:"**",
      data:{},
      dataType :"JSONP",
      type:"GET",
      success:function(activeData) {
          //
      }
  });
```
后端返回如下：
```$xslt
echo $callback ."(".$rd->getJson().")";  //callback通过参数接受

```

这里第一次代码中callback写死是很不推荐的（我这么做是测试阶段基于其他原因），但是问题的关键在于不能写死同一个回调方法名（当可能同时出现多个请求回调时）。

- 遇到问题要善于思考和排查，以及利用网上的资源。
- 这里关于jquery ajax请求的实现原理和问题的真正原因稍后会进行补充。
