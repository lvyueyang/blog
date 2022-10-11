---
title: css3自定义彩色分割线  
tag: CSS  
---  

```css
:after {
    position: absolute;
    content: '';
    left: 0;
    right: 0;
    bottom: 0;
    background: repeating-linear-gradient(-45deg, #ff6c6c 0, #ff6c6c 20%, transparent 0, transparent 25%, #1989fa 0, #1989fa 45%, transparent 0, transparent 50%);
    height: 2px;
    background-size: 80px;
}
```
![彩色分割线实例图片](http://lvyueyang-blog.oss-cn-beijing.aliyuncs.com/article/9cb36870-c6e3-11e9-b5c1-37dc32ada901.png)  
  