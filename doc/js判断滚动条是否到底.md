---
title: js判断滚动条是否到底  
tag: JavaScript,ES6,小示例  
---  

``` js
let scrollTop = document.documentElement.scrollTop || document.body.scrollTop
let clientHeight = document.documentElement.clientHeight || document.body.clientHeight
let scrollHeight = document.documentElement.scrollHeight || document.body.scrollHeight
if (scrollHeight > clientHeight && scrollTop + clientHeight === scrollHeight) {
    console.log('到底了')
}
```  
  