---
title: 纯css美化复选框，单选框，滑动条（range）  
tag: CSS  
---  

``` html
<div class="box">
　　<!-- 复选框type改成checkbox即可 -->
　　<span class="check">
　　　　<input type="radio" name="radio" id="check1">
　　　　<label for="check1"></label>
　　</span>
　　<label for="check1">男</label>
　　<br>
　　<br>
　　<span class="check">
　　　　<input type="radio" name="radio" id="check2">
　　　　<label for="check2"></label>
　　</span>
　　<label for="check2">女</label>
</div>
```
``` css
* {
	margin: 0;
	padding: 0;
}

.box {
	width: 300px;
	height: 100px;
	margin: 100px auto;
}

/*现将input和label放在一个盒子中，使用定位将input放在label下隐藏*/
.check {
	position: relative;
	display: inline-block;
	width: 20px;
	height: 20px;
	margin-right: 5px;
}

.check input {
	display: none;
}

.check label {
	position: absolute;
	width: 16px;
	height: 16px;
	top: 0;
	left: 0;
	border: 2px solid #cacaca;
	border-radius: 50%;
	background: #fff;
}

/*鼠标悬浮样式*/
.check label:hover {
	border-color: #f78642;
}

.check label:after {
	position: absolute;
	content: "";
	width: 8px;
	height: 4px;
	border: 2px solid #cacaca;
	border-top: none;
	border-right: none;
	opacity: 0.4;
	transform: rotate(-45deg);
	top: 4px;
	left: 3px;
}

.check label:hover:after {
	border-color: #f78642;
}

/*重点在这里*/
.check input:checked+label {
	border: 2px solid #f78642;
}

.check input:checked+label:after {
	opacity: 1;
	border: 2px solid #f78642;
	border-top: none;
	border-right: none;
}
```
### range美化

``` css
input[type="range"]{
    width: 300px;
    height: 10px;
    border: 0;
    background-color: #f0f0f0;
    border-radius: 5px;
    position: relative;
    -webkit-appearance: none !important; 
    outline: none;
}
input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: #ff4400;
}
```  
  