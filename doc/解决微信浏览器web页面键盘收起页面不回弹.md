---
title: 解决微信浏览器web页面键盘收起页面不回弹  
tag: JavaScript,BUG解决,移动端,微信  
---  

``` js
;(function () {
    function isWeiXinAndIos() {
        let ua = '' + window.navigator.userAgent.toLowerCase()
        let isWeixin = /MicroMessenger/i.test(ua)
        let isIos = /\(i[^;]+;( U;)? CPU.+Mac OS X/i.test(ua)
        return isWeixin && isIos
    }

    let myFunction
    let isWXAndIos = isWeiXinAndIos()
    if (isWXAndIos) {
        document.body.addEventListener('focusin', () => {
            clearTimeout(myFunction)
        })
        document.body.addEventListener('focusout', () => {
            clearTimeout(myFunction)
            myFunction = setTimeout(function () {
                window.scrollTo({top: 0, left: 0, behavior: 'smooth'})
            }, 200)
        })
    }
})()
```  
  