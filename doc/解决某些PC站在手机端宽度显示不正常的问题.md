---
title: 解决某些PC站在手机端宽度显示不正常的问题  
tag: JavaScript,BUG解决  
---  

> 可以打开控制台查看html标签的宽度，发现不是当前屏幕的宽度，更改下宽度即可；用js控制下

```js
document.getElementsByTagName('html')[0].style.width= window.innerWidth+'px';
window.onresize = function(){
    document.getElementsByTagName('html')[0].style.width= window.innerWidth+'px';
};
```
加入上面这段话即可动态改变html宽度  
  