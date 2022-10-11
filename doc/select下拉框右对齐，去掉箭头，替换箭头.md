---
title: select下拉框右对齐，去掉箭头，替换箭头  
tag: CSS  
---  

## 右对齐
```css
select{
   width:auto;
   direction: rtl;
}
select option { 
　　direction: ltr; 
}
```
## 去掉箭头（不设置背景色会有灰色背景
```css
select{
   appearance:none;
   -moz-appearance:none;
   -webkit-appearance:none;
   background-color: #fff;
   /*设置箭头*/
   background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAJCAYAAAAGuM1UAAAAH0lEQVR42mNgoDnQ13f7TwiTpIkkm0hyHkl+YhhQAABcfyjsqSyTLgAAAABJRU5ErkJggg==") no-repeat scroll right center transparent;
   padding-right: 14px;
}
```
## 清除ie的默认选择框样式，隐藏下拉箭头
```css
select::-ms-expand { 
   display: none;
}
```  
  