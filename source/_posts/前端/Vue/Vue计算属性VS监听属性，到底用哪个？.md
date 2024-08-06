---
title: Vue，计算属性VS监听属性，到底用哪个？
tags: 
  - vue
  - 前端
date: 2020-07-12 22:23:07
permalink: /pages/3fcfd2/
categories: 
  - 前端
---

## 先说结论：

`push`是不会触发计算属性的 setter，就算值改变了也不会触发 setter，只有赋值才会，也就是使用`=`，所以我认为如果不是赋值的 setter 还是用回 watch 吧。

> 前言

我有一个需求，从服务器获取了一个数据，其中一个属性是`inputList`，是一个字符串，将属性值列表以逗号给开，渲染前端的时候要求每个都要取出来，这时候我就需要把他分割成数组了。

返回服务器的字段，是**字符串**，用 `inputList`记录。

姑且**数组**用变量 `attrValArr` 记录。

## 问题

1.当这个数组`attrValArr` 发生变化时，返回服务器的字段 `inputList`也要发生变化

或者

2.当字段 `inputList`发生变化时，数组`attrValArr` 也要发生变化

其实这个需求很简单，用 vue 的**计算属性**不就行了，是可以，但是**计算属性**的 setter 是要`=`才会触发，而`attrValArr`是一个数组，用`push`追加时，是可以让它发生变化，但是返回服务器的字段不会发生变化，这就很尴尬了。

为什么这么说，我们来看下面的代码

## 对象

```js
// 添加类型的表单对象
addAttrForm: {
  // 分类ID
  categoryId: 0,
  // 属性的类型：0规格，1属性
  type: 0,
  // 类型名字
  name: '',
  // 是否支持手动新增
  handAddStatus: 1,
  // 属性值列表，以逗号隔开
  inputList: '',
  // 属性值列表
  attrValArr: [],
  // 控制 添加属性值的输入框 开关
  inputVisible: false,
  // 控制 要添加属性值
  inputValue: ''
}
```

## 错误示范

### 用 computed 来实现效果

```js
methods:{
    //测试案例
    function (newValue) {
      if (newValue) {
          this.addFormAttrValList.push(inputValue)
      }
    }
},
computed: {
  // 规格属性分类列表的规格属性值
  addFormAttrValList: {
    // getter
    get: function () {
      let arr = []
      if (this.addAttrForm.inputList && this.addAttrForm.inputList.length > 0) {
        arr = this.addAttrForm.inputList.split(',')
      }
      return arr
    },
    // setter
    set: function (newValue) {
      console.log('newVal' + newValue)
      if (newValue) {
        this.addAttrForm.inputList = newValue.join(',')
      }
    }
  }
```

但是这里并不会触发 setter，非常愚蠢。

`push`是不会触发计算属性的 setter，就算值改变了也不会触发 setter，只有赋值才会，也就是使用`=`

那么怎么才会触发？下面这样就触发了

```js
//测试案例
function (newValue) {
  if (newValue) {
      let temp = this.addFormAttrValList
      temp.push(inputValue)
      console.log(temp)
      console.log(this.addFormAttrValList)
      this.addFormAttrValList = temp
  }
}
```

通过 console 我可以发现，这个值都是发生变化了，但是还是不会触发计算属性的 setter

只有执行了第 8 行代码后，才会触发计算属性的 setter

这就很难受了，我还是用回 vue 的 watch 吧。

## 正确示例

```js
watch: {
    'addAttrForm.inputList': function (newVal) {
      this.addAttrForm.attrValArr = this.getAttrValBySpilt(newVal)
    },
    'addAttrForm.attrValArr': function (newVal) {
      this.addAttrForm.inputList = newVal.join(',')
    }
  }
```

这样就实现了

（这里要告诉你了，怎么**只监听对象的某一个属性**，而不是监听整个对象，刚才网上搜别人的都不是这样的。。。有时候我只想监听一两个对象的属性，而不是整个对象，这样子开销小，而且**更加优雅**）

其实可以放到服务器处理，缺点就是会增加服务器消耗，而且这个明显是渲染问题，别人服务器的数据库存的就是 inputList 字段，不可能要求别人改数据库吧。（其实后台也是我自己在写- -）
