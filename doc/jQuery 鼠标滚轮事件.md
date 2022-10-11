---
title: jQuery 鼠标滚轮事件  
tag: jQuery  
---  

**使用插件`jquery-mousewheel`**[下载地址](https://github.com/jquery/jquery-mousewheel)   
 
**使用方法**
```js
$('body').mousewheel(function (event, delta) {
    var dir = delta > 0 ? 'Up' : 'Down';
    if (dir == 'Up') {
        console.log('向上滚动');
    } else {
        console.log('向下滚动');
    }
    return false;
});
```  
  