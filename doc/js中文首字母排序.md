---
title: js中文首字母排序  
tag: JavaScript,ES6,小示例,工具函数,排序  
---  

```js
['张三','李四','王五'].sort((a, b) => {
    a.localeCompare(b, 'zh-Hans-CN', {sensitivity: 'accent'})	
})
```
[localeCompare 相关文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)  
  