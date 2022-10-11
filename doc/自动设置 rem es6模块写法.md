---
title: 自动设置 rem es6模块写法  
tag: CSS,Vue,SASS,SCSS  
---  

```js
export default function () {
  let html = document.documentElement;
  function onWindowResize() {
    if (html.getBoundingClientRect().width < 750) {
      html.style.fontSize = html.getBoundingClientRect().width / 10 + "px"；
    } else {
      html.style.fontSize = 75 + "px"；
    }
  }
  onWindowResize();
  window.addEventListener("resize", onWindowResize);
}
// 引入
import rem from '所在目录/rem'
rem(); //执行
```
vue文件中使用
```html
<style lang="scss">
  [@function](/user/function) px2rem($px) {
    $rem: 75px;
    @return ($px/$rem) + rem;
  }
  .box{
    width:px2rem(100px);
  }
</style>  
  