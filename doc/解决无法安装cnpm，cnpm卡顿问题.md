---
title: 解决无法安装cnpm，cnpm卡顿问题  
tag: JavaScript,编译工具,BUG解决,webpack,npm  
---  

``` sh
# 注册模块镜像
npm set registry https://registry.npm.taobao.org  
# node-gyp 编译依赖的 node 源码镜像  
npm set disturl https://npm.taobao.org/dist 
# 清空缓存  
npm cache clean --force  
# 安装cnpm  
npm install -g cnpm --registry=https://registry.npm.taobao.org  
```  
  