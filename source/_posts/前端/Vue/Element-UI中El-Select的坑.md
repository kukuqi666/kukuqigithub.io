---
title: Element-UI中El-Select的坑
date: 2020-08-11 22:29:34
permalink: /pages/a475e3/
categories: 
  - 前端
tags: 
  - vue
  - Element-UI
---

> 前言

在Elemen-UI官方文档中，如果select绑定的值为对象，请务必指定value-key为它的唯一性标示。

例如

~~~vue
<el-select
    v-model="value"
    placeholder="请选择"
    value-key="id"
    @change="handleChange"
    clearable
  >
    <el-option
      v-for="item in options"
      :key="item.id"
      :label="item.name"
      :value="item"
    >
    </el-option>
  </el-select>
~~~



很明显，在

`handleChange(data)`这个方法中，data就是item。



但是我在回显中遇到了问题，我从服务器返回的是serverId

显然，如果直接设置value = serverId或者是错的

因为如果使用了value-key，则data中的value是一个对象

我得想办法让value.id =  serverId，但是如果直接赋值也是错误的，所以需要自定义一个方法

~~~js
/**
     * 设置默认值
     * 如果select绑定的值为对象，请务必指定value-key为它的唯一性标示
     * 如果使用了value-key，则data中的value是一个对象
     */
    setDefaultValue(id) {
      let obj = this.options.filter(item => item.id === id)[0]
      console.log(obj)
      this.value = obj
    }
~~~

如此一来，就搞定了。