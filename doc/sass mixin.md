---
title: sass mixin  
tag: CSS,SASS,SCSS  
---  

## 文字溢出省略号
``` scss
@mixin coveText($num:1){
  @if $num == 1{
    white-space: normal;
    overflow: hidden;
    text-overflow: ellipsis;
  } @else{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: $num;
    overflow: hidden;
  }
}
```
## 0.5像素border
```scss
@mixin borderPart($color,$position:null,$type:solid) {
  position: relative;
  &:before {
    content: '';
    position: absolute;
    width: 200%;
    height: 200%;
    top: 0;
    transform-origin: 0 0;
    transform: scale(0.5, 0.5);
    box-sizing: border-box;
    @if $position == null {
      border: 1px $type $color;
    } @else if $position == top {
      border-top: 1px $type $color;
    } @else if $position == left {
      border-left: 1px $type $color;
    } @else if $position == right {
      border-right: 1px $type $color;
    } @else if $position == bottom {
      border-bottom: 1px $type $color;
    }
  }
}
```  
  