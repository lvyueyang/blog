---
title: vue-cli 3中使用rem  
tag: JavaScript,CSS,Vue,SCSS,移动端,rem  
---  

## 安装依赖
安装`lib-flexible`
```sh
cnpm install --save lib-flexible
```
安装`postcss-px2rem postcss-loader`
```sh
cnpm install --save-dev postcss-loader postcss-px2rem
```
## 引入`lib-flexible`
```js
import 'lib-flexible/flexible.js'
```
## 配置`meta`标签
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0,minimum=1.0,user-scalable=no">
```
## 配置`vue.config.js`
```js
module.exports = {
    css: {
        loaderOptions: {
            css: {
                // options here will be passed to css-loader
            },
            postcss: {
                // options here will be passed to postcss-loader
                plugins: [require('postcss-px2rem')({
                    remUnit: 75
                })]
            }
        }
    }
}
```  
  