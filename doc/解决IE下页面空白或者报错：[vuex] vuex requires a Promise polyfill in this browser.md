---
title: 解决IE下页面空白或者报错：[vuex] vuex requires a Promise polyfill in this browser  
tag: Vue,webpack  
---  

``` js
[vuex] vuex requires a Promise polyfill in this browser
```
**上述错误的原因是不支持 Promise 方法，导致页面出现空白无法加载。**

## 1. 安装 babel-polyfill
```sh
npm i --save  babel-polyfill
```
## 2.在webpack.config.js中入口设置
```js
entry: {
   login: ['babel-polyfill','./src/login.js'],
   com: ['babel-polyfill','./src/com.js'],
   per: ['babel-polyfill','./src/per.js'] 
}
```
> 参考地址： [https://www.cnblogs.com/weiqinl/p/6794612.html](https://www.cnblogs.com/weiqinl/p/6794612.html)  
  