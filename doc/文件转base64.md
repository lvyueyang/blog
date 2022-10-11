---
title: 文件转base64  
tag: JavaScript,base64,ES6,文件处理  
---  

``` js
//文件转base64
const fileOrBase = file => {
  return new Promise((resolve,reject) =>{
    let reader = new FileReader();
    if(typeof reader === 'undefined'){
      //检查浏览器是否支持FileReader
      console.error('您的浏览器不支持上传，请升级您的浏览器');
      return false;
    }
    reader.readAsDataURL(file);
    //读取成功
    reader.onload = (e) =>{
      resolve(reader);
    };
    //读取失败
    reader.onerror = (err) =>{
      reject(reader);
    };
  });
};

export {
  fileOrBase
}
```  
  