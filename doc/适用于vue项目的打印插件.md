---
title: 适用于vue项目的打印插件  
tag: JavaScript,Vue,ES6,打印  
---  

**此方法只适用于现代浏览器，IE10以下就别用了**
``` js
// 使用时请尽量在nickTick中调用此方法
//打印
export default (refs, cb) => {
    let cloneN
    if (Array.isArray(refs)) {
        cloneN = refs[0].cloneNode(true)
    } else {
        cloneN = refs.cloneNode(true)
    }
    const body = document.getElementsByTagName('body')[0]
    cloneN.style.position = 'absolute'
    cloneN.style.zIndex = '9999999999'
    cloneN.style.top = 0
    cloneN.style.left = 0
    cloneN.style.width = '100%'
    cloneN.style.minHeight = '100%'
    cloneN.style.background = '#fff'
    body.appendChild(cloneN)

    const hideClass = '.print-hide-wrap' // 带有此class的标签将会被隐藏
    cloneN.querySelectorAll(hideClass).forEach(item => {
        item.style.display = 'none'
    })

    // 配置样式
    const bt = body.style.cssText
    body.style.overflowY = 'auto'
    body.style.cloneN = 'auto'
    const eld = document.querySelector('.el-dialog__wrapper')
    const dc = eld.style.cssText
    eld.style.display = 'none'
    // 图片全部加载完成后再开始打印
    let imgs = cloneN.getElementsByTagName('img')
    let len = imgs.length
    let ni = 0

    const print = () => {
        ni += 1
        if (ni === len) {
            // 开始打印
            window.print()
            // 还原样式
            body.style = bt
            eld.style = dc
            // 移除节点
            body.removeChild(cloneN)
            // 回调
            if (cb) {
                cb()
            }
        }
    }

    for (let i of imgs) {
        i.onload = () => {
            print()
        }
        i.onerror = () => {
            print()
        }
    }
}

```  
  