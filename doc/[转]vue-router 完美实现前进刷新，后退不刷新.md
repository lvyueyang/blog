---
title: [转]vue-router 完美实现前进刷新，后退不刷新  
tag: Vue,router,转载  
---  

转载地址 [https://www.cnblogs.com/kdcg/p/9376737.html](https://www.cnblogs.com/kdcg/p/9376737.html)
## 1. 创建a,b,c,d四个页面，在路由的meta属性中添加需要缓存的页面标识(isKeepAlive)
```js
import Vue from 'vue'
import Router from 'vue-router'
const HelloWorld = () => import('@/components/HelloWorld')
const A = () => import('@/components/router-return/router-a')
const B = () => import('@/components/router-return/router-b')
const C = () => import('@/components/router-return/router-c')
const D = () => import('@/components/router-return/router-d')

Vue.use(Router)

const routes = [
  {
    path: '/',
    name: 'HelloWorld',
    component: HelloWorld
  }, {
    path: '/a',
    name: 'A',
    component: A
  }, {
    path: '/b',
    name: 'B',
    component: B,
    meta: {
      isKeepAlive: true
    }
  }, {
    path: '/c',
    name: 'C',
    component: C
  }, {
    path: '/d',
    name: 'D',
    component: D
  }
]
```
## 2. 修改app.vue页面
```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <keep-alive>
      <router-view v-if="$route.meta.isKeepAlive"/>
    </keep-alive>
    <router-view v-if="!$route.meta.isKeepAlive"/>
  </div>
</template>
```
## 3. 添加new Router方法的scrollBehavior的回调处理方法
```js
export default new Router({
  routes,
  scrollBehavior (to, from, savedPosition) {
    // 从第二页返回首页时savedPosition为undefined
    if (savedPosition || typeof savedPosition === 'undefined') {
      // 只处理设置了路由元信息的组件
      from.meta.isKeepAlive = typeof from.meta.isKeepAlive === 'undefined' ? undefined : false
      to.meta.isKeepAlive = typeof to.meta.isKeepAlive === 'undefined' ? undefined : true
      if (savedPosition) {
        return savedPosition
      }
    } else {
      from.meta.isKeepAlive = typeof from.meta.isKeepAlive === 'undefined' ? undefined : true
      to.meta.isKeepAlive = typeof to.meta.isKeepAlive === 'undefined' ? undefined : false
    }
  }
})
```  
  