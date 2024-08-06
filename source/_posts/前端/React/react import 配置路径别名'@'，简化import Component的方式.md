---
title: react import 配置路径别名'@'，简化import Component的方式
date: 2021-01-20 13:42:06
permalink: /pages/3b742d/
categories:
  - 前端
  - React
tags:
  - react
  - import
  - 导入
  - 引入
---
## **摘要**

　　在react中，大多数业务逻辑都组件化；极大的减轻了代码的冗余度，如果组件的层次比较深的话，组件的import就比较费劲，在import时使用“../../components/test”的方式，组件的import就会稍显混乱、组件代码不容易维护。为了可高效的、快速的维护组件代码，废弃“../../”的组件引入方式，配置一个组件路径重写的方式引入组件。

## **配置内容**

　　我在之前就介绍过在react中引入less的配置，同样的为了配置一个路径别名，使用customize-cra来覆写webpack底层配置。(配置覆写webpack需要的插件以及第三方库就不在复述，不清楚的可以去参考**[Ant Design](https://ant.design/docs/react/introduce-cn)**官方的配置说明)

### **路径别名重写方式一**

```js
const { override } = require('customize-cra');
const path = require("path");
 
module.exports = override(
     config =>{
         config.resolve.alias = {
             "@": path.resolve(__dirname, "src")
         };
         return config;
     },
);
```

### **路径别名重写方式二**

```js
const { override, addWebpackAlias } = require('customize-cra');
const path = require("path");
 
module.exports = override(
    addWebpackAlias({
        ["@"]: path.resolve(__dirname, "src")
    }),
);
```

## **Example-实例展示**

### **App.js父组件代码**

```js
import React, { useState } ``from` `'react'``import style ``from` `'./App.module.less'``import { Home } ``from` `'@/pages/home'``; ``//@方式引入Home组件` `class` `App extends React.Component {``  ``render() {``    ``return` `(``      ``<div className={style.box}>``        ``<Home name=``'杰瑞与汤姆'``/>``      ``</div>``    ``);``  ``}``}` `export ``default` `App;
```

### **Home.js子组件代码**

```js
import React, { Component } ``from` `'react'``;``import { Button } ``from` `'antd'``;` `export ``class` `Home extends Component {``  ``constructor(props) {``    ``super(props);``    ``this``.state = { };``  ``}``  ``render() {``    ``return` `(``      ``<div>``        ``<Button type=``'danger'``>{``this``.props.name}</Button>``      ``</div>``    ``);``  ``}``}
```

 

## **配置@路径智能提示**

　　在测试过程中，虽然应用了@引入组件的方式，但是在引用过程中没有智能提示组件路径，为了解决智能提示问题，安装Path Intellisence插件来配置提示。

**1、vsCode插件：**

　　Path Intellisence（在插件库中查找并下载插件）

**2、vsCode中setting.json配置插件功能：（打开vscode编辑器设置，在设置中打开setting.json文件）**

```json
// 配置@路径智能提示
  "path-intellisense.mappings": {
    "@": "${workspaceRoot}/src"
  }
```

**3、在项目package.json所在同级目录下创建文件jsconfig.json：**

```json
{
  "compilerOptions": {
      "target": "ES6",
      "module": "commonjs",
      "allowSyntheticDefaultImports": true,
      "baseUrl": "./",
      "paths": {
        "@/*": ["src/*"]
      }
  },
  "exclude": [
      "node_modules"
  ]
}
```



## 来源

本文章摘自于

react import 配置路径别名'@'，简化import Component的方式 - 请给我一杯冰可乐 - 博客园
https://www.cnblogs.com/BlueBerryCode/p/11969804.html

