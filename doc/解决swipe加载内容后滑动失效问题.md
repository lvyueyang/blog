---
title: 解决swipe加载内容后滑动失效问题  
tag: JavaScript,Swiper  
---  

添加如下两个属性：
```js
observer:true,//修改swiper自己或子元素时，自动初始化swiper
observeParents:true//修改swiper的父元素时，自动初始化swiper
```
文档地址：
[https://www.swiper.com.cn/api/Observer/2015/0308/218.html](https://www.swiper.com.cn/api/Observer/2015/0308/218.html)  
  