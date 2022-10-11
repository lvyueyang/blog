---
title: iconfont 批量加入购物车  
tag: JavaScript,icon  
---  

按下F12 > 选择Console > 粘贴下方代码 > 回车  

```js
var ulList = document.querySelector('.collection-detail ul.block-icon-list');
if(confirm('批量加入购物车将会有一定的等待时间，页面将会卡死一段时间，再次执行将会反选，请耐心等候，么么哒！')){
    console.log('%c正在加入购物车中，请稍后...','color:red;font-size:16px');
    ulList.childNodes.forEach(li => {
        li.childNodes[2].childNodes[0].click();
    })
    console.log('%c操作完成','color:red;font-size:30px;');
}
```  
  