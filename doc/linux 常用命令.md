---
title: linux 常用命令  
tag: Linux  
---  

## 添加到全局
```sh
ln -s /opt/nodejs/bin/npm /usr/local/bin/
```
## 配置到系统环境变量
1. 解压到对应目录 例如：
```sh
/opt/node10
```
2. 配置文件
```sh
vi /etc/profile
```
3. 末尾换行添加
```sh
export NODE=/opt/node10
export PATH=$PATH:$NODE/bin
```
4. 立即生效配置
```sh
source /etc/profile
```
## 配置阿里云的yum源

1. 下载repo文件 
``` sh
wget http://mirrors.aliyun.com/repo/Centos-7.repo
```
2. 备份并替换系统的repo文件 
``` sh
cp Centos-7.repo /etc/yum.repos.d/ 
cd /etc/yum.repos.d/ 
mv CentOS-Base.repo CentOS-Base.repo.bak 
mv Centos-7.repo CentOS-Base.repo
```
3. 执行yum源更新命令 
``` sh
yum clean all 
yum makecache 
yum update
```

## 压缩/解压
``` sh
# 解压：
tar xvf FileName.tar
# 压缩：
tar cvf FileName.tar DirName
```

## git  
下面命令会将下次弹框的账号和密码保存起来，永久使用  
``` sh
git config --global credential.helper store
```
如果想要清除该账号和密码，使用如下命令
``` sh
git config --global credential.helper reset
```  
  