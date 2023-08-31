---
title: githubAction使用rsync部署 
tag: github  
---  

## 服务器生成 ssh 私钥
``` sh
ssh-keygen -t rsa -C "bot@github"
# 注意设置名称不要重复
```
## 将私钥追加在authorized_keys文件的末尾中

## github action 配置
``` yml
name: 版本发布

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  deploy:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [16.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm install -g yarn
        
    - name: 安装依赖
      run: yarn
      
    - name: 开始打包
      run: npm run build
      
    - name: 部署
      uses: contention/rsync-deployments@v2.0.0
      with:
        FLAGS: -avzr --delete
        DEPLOY_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
        HOST: ${{ secrets.REMOTE_HOST }}
        USER: ${{ secrets.REMOTE_USER }}
        LOCALPATH: ./dist/*
        REMOTEPATH: 服务端部署目录
```
