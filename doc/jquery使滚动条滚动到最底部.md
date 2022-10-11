---
title: jquery使滚动条滚动到最底部  
tag: jQuery  
---  

```js
$('body').scrollTop($('body')[0].scrollHeight);
//想要加载页面自动到最底部要写入function中使用setTimeout
function top1(){
    $('body').scrollTop($('body')[0].scrollHeight);
};
setTimeout('top1()',100);
```  
  