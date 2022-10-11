---
title: URL转码  
tag: JavaScript  
---  

```js
decodeURIComponent(data).replace(/\+/g,' ');

decodeURIComponent(res.data.data).replace(/\+/g,' ').replace(/&lt;/g,'<').replace(/&gt;/g,'>');
```  
  