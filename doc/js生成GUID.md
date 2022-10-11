---
title: js生成GUID  
tag: JavaScript  
---  

## 方法一：
```js
//JS生成GUID函数,类似.net中的NewID();
function S4() {   
   return (((1+Math.random())*0x10000)|0).toString(16).substring(1);   
}    
function NewGuid() {   
   return (S4()+S4()+"-"+S4()+"-"+S4()+"-"+S4()+"-"+S4()+S4()+S4());   
}
```
## 方法二：
```js
function newGuid(){
　　var guid = "";
　　for (var i = 1; i <= 32; i++){
　　　　var n = Math.floor(Math.random()*16.0).toString(16);
　　　　guid +=   n;
　　　　if((i==8)||(i==12)||(i==16)||(i==20))
　　　　guid += "-";
　　}
　　return guid;    
}
```  
  