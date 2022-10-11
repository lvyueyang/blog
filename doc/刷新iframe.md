---
title: 刷新iframe  
tag: JavaScript,iframe  
---  

```html
<iframe id="frame" src=""></iframe>
```
```js
document.getElementById('frame').contentWindow.location.reload(true)
```  
  