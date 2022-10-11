---
title: 取出富文本中的html标签  
tag: JavaScript,HTML,工具函数  
---  

```js
getSimpleText(html){
    var reg = new RegExp("<.+?>|&nbsp;","g")
    var text = html.replace(reg,'')
    return text
}
```  
  