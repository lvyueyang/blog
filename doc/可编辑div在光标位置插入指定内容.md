---
title: 可编辑div在光标位置插入指定内容  
tag: JavaScript,ES6,工具函数,富文本  
---  

```js
function insertContent(content) {
    if (!content) {
        return
    }
    let sel = window.getSelection()
    if (sel.rangeCount > 0) {
        let range = sel.getRangeAt(0)                   //获取选择范围
        range.deleteContents()                          //删除选中的内容
        let el = document.createElement("div")          //创建一个空的div外壳 
        el.innerHTML = content                          //设置div内容为我们想要插入的内容。
        let frag = document.createDocumentFragment()    //创建一个空白的文档片段，便于之后插入dom树

        let node = el.firstChild
        let lastNode = frag.appendChild(node)
        range.insertNode(frag)                          //设置选择范围的内容为插入的内容
        let contentRange = range.cloneRange()           //克隆选区
        contentRange.setStartAfter(lastNode)            //设置光标位置为插入内容的末尾
        contentRange.collapse(true)                     //移动光标位置到末尾
        sel.removeAllRanges()                           //移出所有选区
        sel.addRange(contentRange)                      //添加修改后的选区
    }
}
```  
  