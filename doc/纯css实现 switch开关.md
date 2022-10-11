---
title: 纯css实现 switch开关  
tag: CSS,SASS,SCSS  
---  

>利用了css3兄弟选择器
```html
<button class="switch">
   <input type="checkbox">
   <span><i></i></span>
</button> 
```
```scss
.switch {
    position: relative;
    width: 50px;
    height: 25px;
    background-color: #fff;
    border: none;
    outline: none;
    i {
        position: absolute;
        left: 0;
        top: 0;
        display: block;
        height: 23px;
        width:23px;
        border-radius: 50%;
        border: 1px solid #dadada;
        background-color: #fff;
        transition: all .2s;
    }
    span {
        position: absolute;
        display: block;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        border: 1px solid #dadada;
        border-radius: 25px;
        z-index: 0;
    }
    input {
        position: absolute;
        top: 0;
        left: 0;
        width: 50px;
        height: 25px;
        margin: 0;
        padding: 0;
        opacity: 0;
        z-index: 9999;
        &:checked + span {
            background-color: #58ad2c;
            border-color: #58ad2c;
        }
        &:checked + span i {
            background-color: #fff;
            border-color: #58ad2c;
            left: 25px;
        }
    }
}
```  
  