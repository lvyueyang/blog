---
title: input输入限制（持续更新）  
tag: JavaScript,HTML  
---  

## 1. 只读文本框内容
```html
<!--  在input里添加属性值 readonly  -->
<input type="text" value="" readonly>
```
## 2. 只能输入数字(有闪动)
```html
<input type="text" onkeyup="value=value.replace(/[^\d]/g,'')" onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\d]/g,''))">
```
## 3. 只能输入英文和数字
```html
<input onkeyup="value=value.replace(/[\W]/g,'')" onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\d]/g,''))">
```
## 4. 只能输入数字和小数点后两位
```html
<input type="text" onkeyup="clearNoNum(this)">
```
```js
function clearNoNum(obj){
　　obj.value = obj.value.replace(/[^\d.]/g,""); //清除"数字"和"."以外的字符
　　obj.value = obj.value.replace(/^\./g,""); //验证第一个字符是数字而不是
　　obj.value = obj.value.replace(/\.{2,}/g,"."); //只保留第一个. 清除多余的
　　obj.value = obj.value.replace(".","$#$").replace(/\./g,"").replace("$#$",".");
　　obj.value = obj.value.replace(/^(\-)*(\d+)\.(\d\d).*$/,'$1$2.$3'); //只能输入两个小数
};
```
## 5. 只能输入整数
```js
function zhengShu(obj){
　　obj.value = obj.value.replace(/[^\d]/g,""); //清除"数字"和"."以外的字符
　　obj.value = obj.value.replace(/^\./g,""); //验证第一个字符是数字而不是
}
```
## 6. 限制文本框输入字数
```html
<form name="form" action="" method="post">
　　<textarea class="editbox2" onkeydown="numPic(this.form.memo,this.form.remLen,10)" onkeyup="numPic(this.form.memo,this.form.remLen,10)" name="memo" cols="45" rows="8" wrap="on"></textarea>
　　<br>共可输入10字，还剩
　　<input class="editbox1" readOnly maxLength="3" size="3" value="10" name="remLen">字。
　　<br>
　　<input class="bottom" type="submit" value=" 提交 " name="submit">
　　<input class="bottom" type="reset" value=" 重置 " name="reset">
</form>
```
```js
function numPic(field, countfield, maxlimit) {
　　if (field.value.length > maxlimit){
　　　　field.value = field.value.substring(0, maxlimit);
　　}else{
　　　　countfield.value = maxlimit - field.value.length;
　　}
};
```  
  