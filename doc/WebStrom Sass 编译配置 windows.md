---
title: WebStrom Sass 编译配置 windows  
tag: IDE,SASS,SCSS  
---  

## 1. 安装Ruby
> [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)

## 2. 安装完成后打开开始菜单
![](https://lvyueyang-blog.oss-cn-beijing.aliyuncs.com/article/999428-20170617012634071-449939425.png)
## 3. 打开后输入
``` sh
gem install sass
```
查看版本 => 出现版本号说明成功
``` sh
sass -v 
```

## 3. 配置webstorm
**在webstorm中settings中搜索file watchers工具，在此工具中添加一个scss的watcher**
![](https://lvyueyang-blog.oss-cn-beijing.aliyuncs.com/article/999428-20170617012948243-1045607512.png)  
  