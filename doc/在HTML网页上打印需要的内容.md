---
title: 在HTML网页上打印需要的内容  
tag: JavaScript,HTML,CSS  
---  

## 1. 在head里面加入下面一段js代码： 
```js
function preview(oper) {
    if (oper < 10) {
        bdhtml = window.document.body.innerHTML;
        //获取当前页的html代码
        sprnstr = "<!--startprint" + oper + "-->";
        //设置打印开始区域
        eprnstr = "<!--endprint" + oper + "-->";
        //设置打印结束区域
        prnhtml = bdhtml.substring(bdhtml.indexOf(sprnstr) + 18);
        //从开始代码向后取html
        prnhtml = prnhtml.substring(0, prnhtml.indexOf(eprnstr));
        //从结束代码向前取html
        window.document.body.innerHTML = prnhtml;
        window.print();
        window.document.body.innerHTML = bdhtml;
    } else {
        window.print();
    }
};
```
## 2. 在所需要打印的代码，用 `<!--startprint1-->` 和 `<!--endprint1-->` 包围着，如下：
```html 
<!--startprint1-->
<!--打印内容开始-->
<div id=sty>
    ...
</div>
<!--打印内容结束-->
<!--endprint1-->
```
## 3. 最后加上一个打印的按钮
``` html
<button type='button' title='打印' onclick='preview(1)'>打印</button>
```

**另外说明一下，在一个HTML页面里面，可以设置多个打印区域，需要改动一下的就只是几个数字就OK了。如：**
在选择第二个区域里面时用<!--startprint2--><!--endprint2-->包围着，而按钮自然也改成对应的preview(2)了。这样第二区域的打印就完成。
还有一点，就是CSS样式表的问题了，打印的效果是不包含背景的打印的，设置时注意一下。`<style media="print">`和`<link media="print">`的用法合理应用，media="print"是不被网页所显示的，只能在打印的效果上存在，可以设置出打印效果和在网页上所显示的不一样。  
  