---
title: jquery放大镜  
tag: JavaScript,jQuery  
---  

``` css
.imgbox {
    position: relative;
    width: 350px;
    height: 350px;
    border: 1px solid #ccc;
    display: flex;
    -ms-align-items: center;
    align-items: center;
    padding: 10px;
    box-sizing: border-box;
}

.img {
    position: relative;
    overflow: hidden;
}

.imgfloat {
    position: absolute;
    width: 150px;
    height: 150px;
    background-color: #ccc;
    opacity: .7;
    left: 0;
    top: 0;
}

.img img {
    width: 100%;
    display: block;
}

.bigimg {
    position: absolute;
    right: -453px;
    top: 0;
    border: 1px solid #ccc;
    width: 450px;
    height: 450px;
}

.bigimg>div {
    position: relative;
    overflow: hidden;
    width: 100%;
    height: 100%;
}

.bigimg img {
    position: absolute;
    display: block;
}
```
```html
<div class="imgbox">
    <div class="img">
        <img src="img2.jpg" alt="">
        <div class="imgfloat"></div>
    </div>
    <div class="bigimg">
        <div>
            <img src="" alt="">
        </div>
    </div>
</div>
<script src="jquery.js"></script>
```
```js
$('.imgbox').hover(function () {
    var src = $(this).find('img').attr('src');
    // 大图中图片的尺寸 放大镜的宽度与容纳大图的盒子的宽度比 = 小图与大图的宽度比
    var w = ($('.bigimg').width() / $('.imgfloat').width()) * $('.img img').width();
    $('.bigimg img').attr('src', src).width(w);
});
$('.img').mousemove(function (event) {
    // 获取鼠标的坐标
    var x = event.clientX;
    var y = event.clientY;
    // 设置放大镜的位置，跟随鼠标
    // （鼠标的距离左边的距离 - 相对父元素距离左边的距离） / 2
    // 注意父元素的相对距离是距离窗口的距离，所以计算时要用offser().left - $(document).scroolLeft();
    // 意思是要距离文档左边的距离减去滚动条的距离就是距离窗口的距离；
    // 距离顶部的距离同理
    // 然后是居中显示鼠标，要将减去放大镜的宽度除以2
    var zx = x - ($(this).offset().left - $(document).scrollLeft()) - ($('.imgfloat').width() / 2);
    var zy = y - ($(this).offset().top - $(document).scrollTop()) - ($('.imgfloat').height() / 2);
    $('.imgfloat').css({
        'left': zx + 'px',
        'top': zy + 'px'
    });
    // 放大镜的left / 小图片的宽 = 大图移动距离/大图的尺寸
    var bx = '-' + zx / $('.img img').width() * $('.bigimg img').width();
    var by = '-' + zy / $('.img img').height() * $('.bigimg img').height();
    $('.bigimg img').css({
        'left': bx + 'px',
        'top': by + 'px',
    });
});
```  
  