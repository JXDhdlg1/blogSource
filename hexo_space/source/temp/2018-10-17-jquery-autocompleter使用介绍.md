---
title: jquery-autocompleter使用介绍
date: 2016-04-17 14:52:58
---
本文分享使用jquery-autocompleter模板。
欢迎讨论和吐槽。

#### 使用场景
在业务中遇到需求希望可以在输入框中输入游戏名称的一部分，然后自动补全出含游戏id-游戏名称的下拉选项供选择。

#### 使用案列
- 业务中的实现代码如下：
```$xslt
var game_id_names = '';
     $.ajax({
         dataType:'json',
         url : 'URL',
         async:false,//这里选择异步为false，那么这个程序执行到这里的时候会暂停，等待
                     //数据加载完成后才继续执行
         success : function(data){
             for(var i=0;i<data.length;i++){
                 var str = '"'+data[i].gameid+','+data[i].gamename+'"';
                 game_id_names += '{"label":'+str+'},';
             }
         }
     });
     game_id_names = eval('['+game_id_names+']');
     $('#nope').autocompleter({
         // marker for autocomplete matches
         highlightMatches: true,
         // object to local or url to remote search
         source: game_id_names,
         // custom template
         template: '{{ label }}',
         // show hint
         hint: true,
         // abort source if empty field
         empty: false,
         // max results
         limit: 20,
     });
 });
```
- 这里分享一个可查看效果的代码样例：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="normalize.css">
    <link rel="stylesheet" href="mains.css">
    <script type="text/javascript" src="http://img.qidian.com/js/jquery-2.1.1.min.js"></script>
    <script src="jquery.autocompleter.js"></script>
</head>
<body>
测试输入框<input id="test-input" placeholder="请输入水果" maxlength="40" />
</body>
<script >
    $(function(){
        var fruits = eval("[{'label':'西瓜'},{'label':'火龙果'},{'label':'西瓜2'},{'label':'西瓜3'}, {'label':'西瓜4'},{'label':'苹果'},{'label':'苹果7'}]");
        $('#test-input').autocompleter({
            // marker for autocomplete matches
            highlightMatches: true,
            // object to local or url to remote search
            source: fruits,
            // custom template
            template: '{{ label }}',
            // show hint
            hint: true,
            // abort source if empty field
            empty: false,
            // max results
            limit: 20,
        });
    });
</script>
</html>
```


#### 使用交流
使用autocompleter模板需要引入jquery.autocompleter.min.js；
引入jquery.autocompleter.css（不然效果难看）；

效果还是不错的，已上实例是非常基本简单的使用，还有更方便、强大的使用方式希望一起交流。

#### 参考地址
[jQuery自动完成插件autocompleter](http://www.jq22.com/jquery-info438)
