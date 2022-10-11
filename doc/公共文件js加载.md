---
title: 公共文件js加载  
tag: JavaScript,HTML  
---  

**头部：例如**
``` h
<header id="header" class="clearfix">
    <a class="col-xs-9">
        <img src="img/lib/logo.png" alt="">
    </a>
    <div class="col-xs-3 nav_tit text-right"><i class="ion-navicon"></i>
        </ <div class="nav_content">
        <ul>
            <li class="active"><a href="">首页</a>
            </li>
            <li><a href="">公司简介</a>
            </li>
            <li><a href="">新闻</a>
            </li>
            <li><a href="">资讯</a>
            </li>
            <li><a href="">导师团队</a>
            </li>
            <li><a href="">项目峰会</a>
            </li>
            <li><a href="">医疗</a>
            </li>
            <li><a href="">视频总汇</a>
            </li>
            <li><a href="">联系我们</a>
            </li>
        </ul>
    </div>
</header>
```
**改为js模板：**
```js
document.write('<header id="header" class="clearfix"><a class="col-xs-9"><img src="img/lib/logo.png" alt=""></a><div class="col-xs-3 nav_tit text-right"><i class="ion-navicon"></i></div><div class="nav_content"><ul><li class=""><a href="">首页</a></li><li><a href="">公司简介</a></li><li><a href="">新闻</a></li><li><a href="">资讯</a></li><li><a href="">导师团队</a></li><li><a href="">项目峰会</a></li><li><a href="">医疗</a></li><li><a href="">视频总汇</a></li><li><a href="">联系我们</a></li></ul></div></header>');

//控制样式
(function () {
    var header_module  = document.getElementById('header_module');
    var header = document.getElementById('header');
    var nav = header.getElementsByClassName('nav_content')[0];
    var li = nav.getElementsByTagName('li');
    var a = nav.getElementsByTagName('a');
    var index = header_module.getAttribute('data-active');
    li[index].className = 'active';
    a[0].setAttribute('href','index.html');  //添加href
})();
```
**引入js文件：注意给标签写上id**
```html
// data-active 为控制导航选中的样式
<script id="header_module" src="js/header.js" data-active="0"></script>
```
> html代码在线压缩：(http://tool.oschina.net/jscompress?type=2)[http://tool.oschina.net/jscompress?type=2]  
  