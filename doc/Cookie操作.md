---
title: Cookie操作  
tag: JavaScript,Cookie  
---  

```js
var Cookie = {
    set: function (name, value, days) {
        // 写入
        var days = days || 1; //默认1天
        var d = new Date;
        d.setTime(d.getTime() + 24 * 60 * 60 * 1000 * days);
        window.document.cookie = name + "=" + value + ";path=/;expires=" + d.toGMTString();
    },
    get: function (name) {
        // 获取
        var v = window.document.cookie.match('(^|;) ?' + name + '=([^;]*)(;|$)');
        return v ? v[2] : null;
    },
    delete: function (name) {
        // 删除
        this.set(name, '', -1);
    }
};
```  
  