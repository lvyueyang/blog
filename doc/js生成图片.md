---
title: js生成图片  
tag: JavaScript,图片处理,canvas  
---  

```js
var image = new Image();
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
var img = document.getElementById("scream");
ctx.font = "10px Arial";

function createImg(name, zuowei, color) {
    //  姓名
    ctx.fillText(name, 93, 373);
    ctx.fillText(name, 393, 370);
    //  座位号
    ctx.font = "bold 20px Arial";
    ctx.fillText(zuowei, 216, 350);
    ctx.fillText(zuowei, 393, 350);
    //  座位颜色
    ctx.font = "bold 20px Arial";
    ctx.fillText(color, 264, 350);
    ctx.fillText(color, 441, 350);
    //  生成图片
    image = c.toDataURL("image/png");
    return image;
}

ctx.drawImage(img, 0, 0, 550, 520);
var src = createImg(name, zuowei, color);
$('#box').attr('src', src);
```  
  