---
title: 数据库model书写规范  
tag: Node,egg,MongoDB  
---  

### 1. 表示数据状态，或者类型的，不做数学运算，使用`String`
### 2. 表示数据类型使用`type`，表示数据状态使用`state`
``` js
{
  type: '表示类型',
  state: '表示状态',
  auth: '作者',
  createAt: '创建时间',
  undateAt: '更新时间',
  desc: '表示描述',
  content: '表示完整详情',
  _id: '表示数据id',
  delete: '表示是否已被软删除 Boolean 类型'
}  
  