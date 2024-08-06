---
title: Element UI中Switch 开关的小坑，如何使用0和1或其他？
tags: 
  - 前端
  - vue
  - Element-UI
date: 2020-07-12 19:46:33
permalink: /pages/472b2f/
categories: 
  - 前端
---

> 前言

根据后台传值动态显示开关（0为关，1为开）,其绑定字段是`scope.row.handAddStatus`

Swich默认是boolean类型，而后台传值 为number类型，这个时候我想用number来取代boolean类型



## **错误**示范：

```vue
<el-switch v-model="scope.row.handAddStatus"
                           active-value="1"
                           inactive-value="0"
                           disabled
                           active-color="#13ce66"
                           inactive-color="#ff4949">
                </el-switch>

```

很明显实现不了，为什么？

`active-value`和`inactive-value`的值分别是字符串的1和2
如果你赋值为数字类型的 1 或 2是无法正常工作的



## 解决方法

若赋值为数值类型，需这样写：
```vue
<el-switch v-model="scope.row.handAddStatus"
                           :active-value="1"
                           :inactive-value="0"
                           disabled
                           active-color="#13ce66"
                           inactive-color="#ff4949">
                </el-switch>
```

看到区别了嘛，原来`active-value`和`inactive-value`的前面，要加**分号**，才能识别是数字类型



那么以后我需要记住，字符串直接赋值，而数字类型要加`;`