---
title: Element-UI 级联选择框回显问题
date: 2020-08-11 22:37:59
permalink: /pages/65084e/
categories: 
  - 前端
tags: 
  - vue
  - Element-UI
---

## 前言

在ElementUI中，级联选择框的v-model是一个数组，存的是id数组

但是我服务器存的是数组的最后一个id，那么如何才能回显？



~~~js
data() {
    return {
      // 分类的树结构数据列表
      cateList: [],
      // 已选择分类ID数组
      selectCateKeys: []
    }
  }
~~~





如下代码

~~~vue
<el-cascader
    v-model="selectCateKeys"
    :options="cateList"
    ref="cateListRef"
    width="auto"
    :show-all-levels="showAllLevels"
    filterable
    :props="{
      expandTrigger: 'hover',
      value: 'id',
      label: 'name',
      children: 'children'
    }"
    clearable
    @change="selectCateChange"
  >
  </el-cascader>
~~~





## 思路

服务器返回一个id，我从树结构数据中，把他的父级id都查出来

~~~js
/**
     * 设置选定值
     */
    setSelectCateKeys(id) {
      this.selectCateKeys.splice(0)
      let keys = this.find(this.cateList, id)
      this.selectCateKeys = keys
    },
    /**
     * 递归，通过子级Id向上找到所有的父级id
     */
    find(array, id) {
      let stack = []
      let going = true
      let walker = (array, id) => {
        array.forEach(item => {
          if (!going) return
          stack.push(item['id'])
          if (item['id'] === id) {
            going = false
          } else if (item['children']) {
            walker(item['children'], id)
          } else {
            stack.pop()
          }
        })
        if (going) stack.pop()
      }
      walker(array, id)
      return stack
    },
~~~



很明显，我现在找到了id数组，数据已经是正确了，但是问题又来了，Element-UI中，根本不会回显文本`name`，我点击己联选择框进去，发现已经选择了，就是文本没有回显，所以我再定义多一个方法

~~~js
/**
     * 设置选定值
     */
    setSelectCateKeys(id) {
      this.selectCateKeys.splice(0)
      let keys = this.find(this.cateList, id)
      this.selectCateKeys = keys
      let name = this.findName(this.cateList, id).join(' / ')
      this.$refs.cateListRef.inputValue = name
    },
    /**
     * 递归，通过id查找名字
     */
    findName(array, id) {
      let name = []
      let going = true
      let walker = (array, id) => {
        array.forEach(item => {
          if (!going) return
          name.push(item['name'])
          if (item['id'] === id) {
            going = false
          } else if (item['children']) {
            walker(item['children'], id)
          } else {
            name.pop()
          }
        })
        if (going) name.pop()
      }
      walker(array, id)
      return name
    },
    /**
     * 递归，通过子级Id向上找到所有的父级id
     */
    find(array, id) {
      let stack = []
      let going = true
      let walker = (array, id) => {
        array.forEach(item => {
          if (!going) return
          stack.push(item['id'])
          if (item['id'] === id) {
            going = false
          } else if (item['children']) {
            walker(item['children'], id)
          } else {
            stack.pop()
          }
        })
        if (going) stack.pop()
      }
      walker(array, id)
      return stack.join
    },
~~~



![image-20200813225505305](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/225506-734368.png)

这里商品分类**手机数码 / 手机通讯 / 5G手机**是从前台获取的，后台就存了对象的id



暂时就这样做到了文本显示，虽然有些粗暴，但是将就着先，



## TODO

还是有一个小bug，当我点击商品分类时，如果我不选择，文本全部消失了，这个挖坑吧，而且验证也能通过，说明数据已经是对的，但是就是文本的问题，一般来说，影响不大，将来再解决。
