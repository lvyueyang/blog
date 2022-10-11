---
title: vue，微信小程序，验证码倒计时摁扭  
tag: Vue,ES6,小程序,小示例  
---  

## Vue
```html
<template>
    <button type="button" :disabled="btn.disabled" @click="getYzmFn">{{btn.text}}</button>
</template>
<script>
    export default {
        name: 'YZNButton',
        data() {
            return {
                btn: {
                    text: '发送验证码',
                    time: 60,
                    timeFn: null,
                    disabled: false
                }
            }
        },
        methods: {
            getYzmFn() {
                let btn = this.btn
                const sTime = btn.time
                btn.disabled = true
                btn.time -= 1
                btn.text = `${btn.time}S后重新发送`
                btn.timeFn = setInterval(() => {
                    btn.time -= 1
                    btn.disabled = true
                    if (btn.time <= 0) {
                        clearInterval(btn.timeFn)
                        btn.text = `发送验证码`
                        btn.disabled = false
                        btn.time = sTime
                        return false
                    }
                    btn.text = `${btn.time}S后重新发送`
                }, 1000)
            }
        }
    }
</script>


```

## 小程序
``` html
<button class='btn {{btn.disabled ? "disabled" : ""}}' disabled="{{btn.disabled}}" bindtap="getYzmFn">{{btn.text}}</button>
```
```js
data: {
    btn: {
        text: '发送验证码',
        time: 60,
        timeFn: null,
        disabled: false
    }
},
getYzmFn() {
    let btn = this.data.btn
    const sTime = btn.time
    btn.time -= 1
    this.setData({
        'btn.disabled': true,
        'btn.time': btn.time,
        'btn.text': `${btn.time}S后重新发送`
    })
    btn.text = `${btn.time}S后重新发送`
    btn.timeFn = setInterval(() => {
        btn.time -= 1
        this.setData({
            'btn.disabled': true,
            'btn.time': btn.time,
        })
        if (btn.time <= 0) {
            clearInterval(btn.timeFn)
            this.setData({
                'btn.disabled': false,
                'btn.text': '发送验证码',
                'btn.time': sTime
            })
            return false
        }
        this.setData({
            'btn.text': `${btn.time}S后重新发送`
        })
    }, 1000)
}
```  
  