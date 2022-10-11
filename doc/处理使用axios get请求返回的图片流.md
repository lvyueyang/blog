---
title: 处理使用axios get请求返回的图片流  
tag: JavaScript,base64,图片处理,ES6  
---  

``` js
axios.get('/v1.0/captcha/captchaImagePC?type=math', {
    responseType: 'arraybuffer'
}).then(res => {
    return 'data:image/png;base64,' + btoa(new Uint8Array(res).reduce((data, byte) => data + String.fromCharCode(byte), ''))
})
```  
  