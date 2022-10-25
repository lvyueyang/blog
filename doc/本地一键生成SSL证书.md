---
title: 本地使用一键生成SSL证书 
tag: SSL  
---  

## 用到的工具  
https://github.com/FiloSottile/mkcert

## 下载
进入 release 页下载对应软件 https://github.com/FiloSottile/mkcert/releases

## win 安装 
``` sh
# 可以将文件拖入到 cmd 中 后面加 -install 回车即可
{下载的文件所在路径}\mkcert-v1.4.4-windows-amd64.exe -install
```
## 生成证书
``` sh
# 将上方的 -install 替换为 host 即可，多个使用空格分隔
{下载的文件所在路径}\mkcert-v1.4.4-windows-amd64.exe 127.0.0.1 localhost
```
