---
title: vue项目搭建过程
date: 2020-08-13 13:07:13
permalink: /pages/0ca752/
categories:
  - 前端
tags:
  - vue
  - 项目实战
  - 搭建过程
---
> 前言

由于我之前的前端项目，不统一，而且也不规范，现在重新搭建一下。

参考：

徐丽健. Spring Boot+Spring Cloud+Vue+Element项目实战：手把手教你开发权限管理系统 (Kindle 位置 2439-2441). 清华大学出版社. Kindle 版本.

## 搭建开发环境

所需工具：

### VScode

Visual Studio Code 是微软产品的一款开源编辑器，非常优秀轻量化。

### Node Js

Node JS 提供 的 NPM 依赖 管理 和 编译 打包 工具 使用 起来 非常 方便， 对于 前端 比较 大型 一些 的 项目 还是 采用 NPM 作为 打包 工具 比较 理想。 要 使用 NPM， 就 需要 安装 NodeJS， 下载 地址 为 http:// nodejs. cn/ download/。

把 Node 添加 到 系统 环境 变量 里面， 打开 cmd 命令行， 输入 npm -v，就可以查看到版本信息，就说明已经安装正确。

如果是旧版，也可以通过npm命令来升级。

```bash
# linux 系统命令
sudo npm install npm -g
# windows 系统命令
npm install npm -g
```

安装好NPM之后，就可以用NPM命令来下载各种工具了。

### 淘宝镜像

NPM是国外的中央仓库，国内访问速度可能比较慢，所以就需要国内镜像，就像MAVEN一样。

NPM国内镜像一般使用淘宝镜像。

如果在国外就无视这条吧。

```bash
npm install -g cnpm --registry=https://registry.npm.tao.org
```

安装成功后，以后就用CNPM代替NPM命令了，比如

```bash
cnpm install webpack -g
```

### Yarn

Yarn 是 Facebook 发布 的 node. js 包 管理器， 比 npm 更快、 更 高效， 可以 使用 Yarn 替代 npm。 安装 了 Node， 同时 也就 安装 了 NPM， 可以 使用 下面 的 命令 来 安装：

```bash
npm i yarn -g -verbose
```

实际上，yarn也有淘宝镜像。

```bash
yarn config set registry https://registry.npm.taobao.org
```

Yarn跟NPM差别不大，例如：

```bash
npm install

yarn install

npm install --save [package]

yarn add [package]

npm install --save-dev [package]

yarn add [package] --dev

npm install --global [package]

yarn global add [package]

npm unistall --save [package]

yarn remove [package]

npm unistall --save-dev [package]

yarn remove [package]

yarn global add @vue/cli-init
```

是不是yarn更加简洁了？

### webpack

webpack是一个打包工具，之后要用到它，这里安装也行，后面记得回来安装，我这里就先安装了。

```bash
#yarn安装方式
yarn global add webpack
```

> 参考资料

http:// www. runoob. com/ w3cnote/ webpack- tutorial. html

### vue-cli

vue脚手架项目初始化工具vue-cli，这个必须安装

```bash
yarn global add @vue/cli
```

到这里基本环境已经搭建完成，下面开始创建项目。

## 搭建项目脚手架

> 参考资料

[https://juejin.im/post/5d615cdcf265da03a715de23](https://juejin.im/post/5d615cdcf265da03a715de23)

### vue create

打开vscode，打开终端，cd命令切换到想要创建目录的地方.

通过vue-cli来生成一个项目，下面name是想要的项目名字。

```bash
vue create [name]
```

然后就会有选项

- `vue_web_preset(babel,route,eslint)` vue网页准备
- `default (babel, eslint)` 默认配置 提供babel和eslint支持
- `Manually select features` 自己手动去选择需要的配置

这里，选择手动去配置。（上下方向键来操控，回车确定）

然后又出现选择了。

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232917-523239.png)

对于每一项的功能，做一下简单阐述：

- `Babel` 主要是对es6语法转换成兼容的js （选上）
- `TypeScript` 支持使用TypeScript语法来编写代码
- `PWA` [PWA](https://developers.google.com/web/progressive-web-apps/) 支持
- `Router` 支持vue路由配置插件（一般都会选择）
- `Vuex` 支持vue程序状态管理模式 (一般都会选择)
- `CSS Pre-processors` 支持css预处理器 （一般都会选择）
- `Linter / Formatter` 支持代码风格检查和格式化 （选上）
- `Unit Testing` 单元测试
- `E2E Testing` E2E测试

选择内容如下：（**空格选择**）

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%201.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232933-103339.png)

选择完成后回车：

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%202.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232931-829709.png)

这的意思是问你本次项目是否采用history模式，如果选择Y,需要后台配置具体看vueRouter官网解释，这里选择 n

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%203.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232935-596794.png)

这里是问你选择一种css预处理，我项目一般使用SCSS，所以这块我选择第一个，回车后

> scss参考：[https://www.sass.hk/guide/](https://www.sass.hk/guide/)

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%204.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232941-867331.png)

这里是问你选择一种格式化代码方式，我用VSCode，所以一般选择 `ESlint + Prettier`,选择回车：

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%205.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232944-263737.png)

这里问你什么时候进行代码规则检测，一般会选择保存就检测，也就是`Lint on save` 选择回车：

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%206.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232946-60062.png)

这问将Babel,PostCSS,ESLint这些配置文件放哪，通常我们会选择放到独立位置，让package.json文件干净点，所以选择**第一个** 点击回车：

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%207.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232948-402409.png)

这里是问你是否记录这次配置选择，选择之后会让你为这次配置起一个名字，这样下次可以直接快速配置选择，最后回车后就会初始化项目了，完成后如下图：

输入一个名字，然后按回车

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%208.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232949-735988.png)

### 安装依赖

按照提示cd切换到目录

然后执行

```bash
yarn install
```

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%209.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232955-661450.png)

安装好了后，目录如下：

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%2010.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232957-32820.png)

vscode插件安装live server

## 启动运行项目

```bash
yarn serve
```

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%2011.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/232959-860548.png)

到此已经搭建完了，下面进行项目的环境搭建。

接下来命令都在项目中执行

## 新建用户代码片段

配置代码片段是为了快速开发

首页>>首选项>>用户片段>>新建

```json
{
    "Print to console": {
        "prefix": "vue",
        "body": [
            "<template>",
            "  <div>\n",
            "  </div>",
            "</template>\n",
            "<script>",
            "export default {",
            "  data() {",
            "    return {\n",
            "    }",
            "  },",
            "  methods: {\n",
            "  },",
            "  components: {\n",
            "  }",
            "}\n",
            "</script>\n",
            "<style lang='scss'>\n",
            "</style>",
            "$2"
        ],
        "description": "创建一个自定义的vue组件代码块"
    }
}
```

配置完，在写页面输入vue就可以看到了。



## 导入项目

### Element-UI

#### 安装依赖

```bash
yarn add element-ui
```

#### 导入项目

在main.js中引入

```jsx
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

Vue.use(ElementUI)
```

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%2012.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233210-475273.png)

#### VScode安装插件 Element UI Snippets

直接搜名字安装，这个是语法提示

### 测试

安装好了之后，去HelloWorld.vue随便输入一个标签测试一下是否引入成功。

```html
<el-button type="primary">测试按钮</el-button>
```

 views 目录 下 添加 3 个 页面： Login. vue、 Home. vue、 404. vue。 3 个 页面 内容 简单 相似， 只有 简单 的 页面 标识， 如 登录 页面 是“ Login Page”。 Login. vue 代码 如下， 其他 页面 类似。

```html
<template>
  <div>
    Login
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {

  },
  components: {

  }
}

</script>

<style lang='scss'>
</style>
```

###  配置路由

打开 router/ index. js， 添加 3 个 路 由， 分别 对应 主页、 登录 和 404 页面。

#### router/index.js

```jsx
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
  {
    path: '/home',
    name: 'Home',
    component: () => import('@/views/Home.vue'),
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('@/views/About.vue'),
  },
  {
    path: '/login',
    name: 'Login',
    component: () => import('@/views/Login.vue'),
  },
  {
    path: '/404',
    name: 'notFound',
    component: () => import('@/views/404.vue'),
  },
]

const router = new VueRouter({
  routes,
})

export default router
```

#### 测试

配置完在app.vue测试一下，是否访问正常

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/home">Home</router-link> |
      <router-link to="/login">Login</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/404">404</router-link>

    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
```

**404.vue**

```html
<template>
  <div>
    404
    <p>
      <el-button @click="$router.go(-1)">返回上一页</el-button>
      <el-button type="primary"
                 @click="$router.push('/home')">进入首页</el-button>

    </p>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {

  },
  components: {

  }
}

</script>

<style lang='scss'>
</style>
```

全部都能访问说明正常。



### 安装scss

~~~bash
yarn add sass-loader
yarn add node-sass
~~~



### axios

axios 是一 个 基于 Promise 用于 浏览器 和 Node. js 的 HTTP 客户 端， 我们 后续 需要 用来 发送 HTTP 请求， 接下 讲解 axios 的 安装 和 使用。

#### 安装依赖

```json
yarn add axios
```

#### 测试

安装后编写home.vue测试

HelloWorld.vue

```html
<template>
  <div>
    <el-button type="primary"
               @click="testAxios">testAxiosBtn</el-button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {

    }
  },
  methods: {
    testAxios () {
      axios.get('http://localhost:8080').then(res => { alert(res.data) })
    }
  },
  components: {

  }
}

</script>

<style lang='scss'>
</style>
```

测试结果

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%2013.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233217-753701.png)

### Mock

为了模拟后台接口提供页面需要的数据，引入Mock.js为我们提供模拟数据，而不用依赖于后台接口的完成。

#### 安装依赖

```bash
yarn add mockjs -dev
```

#### 编写代码

在src目录下新建mock目录，创建mock.js，模拟两个接口，分别拦截用户和菜单的请求，并返回响应数据。

mock.js

```bash
import MOck from 'mockjs'

Mock.mock('http://localhost:8080/user', {
  name: '@name', //随机生成名字
  name: '@email', //随机生成邮箱
  'age|1-10': 5, //年龄在1~10岁之间
})

Mock.mock('http://localhost:8080/menu', {
  id: '@increment', //id自增
  name: 'menu', //名称为menu
  'order|1-20': 5, //排序在1~20之间
})
```

Home.vue

```html
<template>
  <div class="home">
    <img alt="Vue logo"
         src="@/assets/logo.png" />
    <el-button type="primary"
               @click="testAxios">testAxiosBtn</el-button>
    <el-button type="primary"
               @click="testUser">testUser</el-button>
    <el-button type="primary"
               @click="testMenu">testMenu</el-button>
    <el-button type="primary"
               @click="test">test</el-button>

  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import mock from '@/mock/index.js'

export default {
  name: "Home",
  methods: {
    test () {
      axios.get("http://localhost:8080/test")
        .then(res => {
          console.log(res.data);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    // testAxios () {
    //   axios.get('http://localhost:8080').then(res => { alert(res.data) })
    // },
    // testUser () {
    //   axios.get('http://localhost:8080/user').then(res => { alert(JSON.stringify(res.data)) })
    // },
    // testMenu () {
    //   axios.get('http://localhost:8080/menu').then(res => { alert(JSON.stringify(res.data)) })
    // }
  },
  components: {
  }
};
</script>
```

#### 解决BUG

突然看到报错，这里报什么错，回到控制台看到。

![Untitled%20bfaef6c4010e4d1e96ee80690d76e678/Untitled%2014.png](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233231-575878.png)

这里我复制运行代码，再另一个窗口运行

```bash
npm install --save mockjs
```

然后我再重新运行服务器

```bash
yarn run serve
```

发现还是报错了

![image-20200716064136589](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233236-308629.png)

按照提示

~~~bash
npm install --save core-js/modules/es.object.to-string
~~~

还是报错

![image-20200716064406993](D:\Projects\vuepress-theme-vdoing\docs\05.前端\VUE前端实现项目管理平台.assets\image-20200716064406993.png)

想了想，是不是我安装依赖出了，问题，于是我把`node_moudles`整个文件夹给删除了。

重新执行

~~~bash
yarn install
~~~



![image-20200716064618731](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233241-357769.png)



执行成功后，我再来执行

~~~bash
yarn run serve
~~~

还是报错



![image-20200716064706590](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233030-766916.png)



决定打开vue ui界面看看

执行

~~~bash
vue ui
~~~



导入项目

![image-20200716065256718](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233310-733203.png)

选择rebuild

编译运行。

![image-20200716065325998](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233033-521747.png)



搜索一番。

#### 配置.prettierrc文件

在项目根目录下的`.prettierrc`文件中写入即可。其实就是不让`prettier`检测文件每行结束的格式.

```
{
  "endOfLine": "auto" 
  // 是否在结尾加分号
  "semi": false,
  // 是否使用单引号
    "singleQuote": true
}
```

缺点：不能兼容跨平台开发，从前端工程化上讲没有做到尽善尽美。



然而还是出错了

![image-20200716065637882](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233328-934213.png)



看到这里

> https://github.com/vuejs/vue-cli/issues/2873

我决定试下



我把控制台清了

![image-20200716070029137](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233332-634713.png)



原来已经能正常访问。。。。这个坑留着吧，看到issue都没解决。



在成功访问后，我发现还是存在错误

![image-20200716083523745](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233337-341721.png)



事实上，这个错误根本不算。

> 解决方法

找到`.eslintrc.js`文件，在`rules`里面添加上如下代码，就可以去掉提示了。

```js
"no-unused-vars": 'off'
```

![image-20200716083615005](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233341-659024.png)



最后我们修改home.vue代码如下：

~~~vue
<template>
  <div class="home">
    <img alt="Vue logo" src="@/assets/logo.png" />
    <el-button type="primary" @click="testAxios">testAxiosBtn</el-button>
    <el-button type="primary" @click="testUser">testUser</el-button>
    <el-button type="primary" @click="testMenu">testMenu</el-button>
    <el-button type="primary" @click="test">test</el-button>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import mock from "@/mock/index.js";

export default {
  name: "Home",
  methods: {
    test() {
      axios
        .get("http://localhost:8080/test")
        .then(res => {
          console.log(res.data);
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    testAxios() {
      axios.get("http://localhost:8080").then(res => {
        console.log(res.data);
      });
    },
    testUser() {
      axios.get("http://localhost:8080/user").then(res => {
        console.log(JSON.stringify(res.data));
      });
    },
    testMenu() {
      axios.get("http://localhost:8080/menu").then(res => {
        console.log(JSON.stringify(res.data));
      });
    }
  },
  components: {}
};
</script>

~~~



运行结果：

![image-20200716083731256](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233345-769194.png)

说明mock已经集成进来了。





## 工具模块封装

### 封装axios模块

#### 封装背景

使用 axios 发起 一个 请求 是 比较 简单 的 事情， 但是 axios 没有 进行 封装 复 用， 项目 越来越大， 会 引起 越来越多 的 代码 冗余， 让 代码 变得 越来越 难 维护， 所以 我们 在这里 先 对 axios 进行 二次 封装， 使 项目 中 各个 组件 能够 复 用 请求， 让 代码 变得 更容易 维护。



#### 封装要求

- 统一url配置
- 统一api请求
- request（请求）拦截器。例如；带上token等，设置请求头。
- response（响应）拦截器。例如：统一错误处理，页面重定向等。
- 根据需要，结合vuex做全局的loading动画



#### global.js

在src目录下,新建一个`utils`文件夹，用来存放全局常量

~~~js
/**
 * 全局常量，方法封装模块
 * 通过原型挂载到Vue属性
 * 通过this.global调用
 */

//后台服务器地址
export const baseUrl = 'http://localhost:9527'

//系统数据备份还原服务器地址
export const backupBaseUrl = 'http://localhost:8002'

export default {
  baseUrl,
  backupBaseUrl
}

~~~



#### 安装js-cookie

会用 到 Cookie 获取 token， 所以 需要 把 相关 依赖 安装 一下。 执行 以下 命令， 安装 依赖 包，

~~~bash
yarn add js-cookie
~~~

![image-20200716095642436](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233348-880465.png)



在`utils`新建`auth.js`

~~~js
import Cookies from 'js-cookie'

const TokenKey = 'loginToken'

export function getToken() {
  return Cookies.get(TokenKey)
}

export function setToken(token) {
  return Cookies.set(TokenKey, token)
}

export function removeToken() {
  return Cookies.remove(TokenKey)
}
~~~





#### http文件夹说明

在 src 目录 下， 新建 一个 http 文件夹， 用来 存放 http 交互 api 代码。 

文件 结构 如下： 

- config. js：axios 默认 配置， 包含 基础 路径 等 信息 。 
- axios. js： 二次 封装 axios 模块， 包含 拦截 器 等 信息。 
- api. js ：请求 接口 汇总 模块， 聚合 所有 模块 API。 
- index. js： 将 axios 封装 成 插件， 按 插件 方式 引入。 
- modules（文件夹）： 用户 管理、 菜单 管理 等 子 模块 API。



如图所示：

![image-20200716084715717](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233352-197446.png)



#### config.js

axios 默认 配置， 包含 基础 路径 等 信息

~~~js
import { baseUrl } from '@/utils/global'

export default {
  method: 'get',
  //基础url前缀
  baseUrl: baseUrl,
  //请求头信息
  headers: {
    'Content-Type': 'application/json;charset=UTF-80'
  },
  //参数
  data: {},
  //设置超时时间
  timeout: 10000,
  //携带凭证
  withCredentials: true,
  //返回数据类型
  responseType: 'json'
}

~~~



#### axios.js

axios 拦截 器， 可以 进行 请求 拦截 和 响应 拦截， 在 发送 请求 和 响应 请求 时 执行 一些 操作。 

1. 这里 导入 类 配置文件 的 信息（ 如 baseURL、 headers、 withCredentials 等 设置） 到 axios 对象。 
2. 发送 请求 的 时候 获取 token， 如果 token 不存在， 说明 未 登录， 就 重定 向到 系统 登录 界面， 否则 携带 token 继续 发送 请求。 
3. 如果 有 需要， 可以 在这里 通过 response 响应 拦截 器 对 返回 结果 进行 统一 处理 后再 返回。



~~~js
import axios from 'axios'
import config from '@/http/config'
import { getToken } from '@/utils/auth'
import router from '@/router'

export default function $axios(options) {
  return new Promise((resolve, reject) => {
    const instance = axios.create({
      baseURL: config.baseUrl,
      headers: config.headers,
      timeout: config.timeout,
      withCredentials: config.withCredentials
    })
    // request 请求拦截器
    instance.interceptors.request.use(
      config => {
        let token = getToken()
        // 发送请求时携带token
        if (token) {
          config.headers['Authorization'] = token
        }
        // 暂时注销，与导航守卫冲突
        // else {
        //   // 重定向到登录页面
        //   router.push('/login')
        // }
        return config
      },
      error => {
        // 请求发生错误时
        console.log('request:', error)
        // 判断请求超时
        if (
          error.code === 'ECONNABORTED' &&
          error.message.indexOf('timeout') !== -1
        ) {
          console.log('timeout请求超时')
        }
        // 需要重定向到错误页面
        const errorInfo = error.response
        console.log(errorInfo)
        if (errorInfo) {
          error = errorInfo.data // 页面那边catch的时候就能拿到详细的错误信息,看最下边的Promise.reject
          const errorStatus = errorInfo.status // 404 403 500 ...
          router.push({
            path: `/error/${errorStatus}`
          })
        }
        return Promise.reject(error) // 在调用的那边可以拿到(catch)你想返回的错误信息
      }
    )

    // response 响应拦截器
    instance.interceptors.response.use(
      response => {
        return response.data
      },
      err => {
        if (err && err.response) {
          switch (err.response.status) {
            case 400:
              err.message = '请求错误'
              break
            case 401:
              err.message = '未授权，请登录'
              break
            case 403:
              err.message = '拒绝访问'
              break
            case 404:
              err.message = `请求地址出错: ${err.response.config.url}`
              break
            case 408:
              err.message = '请求超时'
              break
            case 500:
              err.message = '服务器内部错误'
              break
            case 501:
              err.message = '服务未实现'
              break
            case 502:
              err.message = '网关错误'
              break
            case 503:
              err.message = '服务不可用'
              break
            case 504:
              err.message = '网关超时'
              break
            case 505:
              err.message = 'HTTP版本不受支持'
              break
            default:
          }
        }
        console.error(err)
        return Promise.reject(err) // 返回接口返回的错误信息
      }
    )
    // 请求处理
    instance(options)
      .then(res => {
        resolve(res)
        return false
      })
      .catch(error => {
        reject(error)
      })
  })
}

~~~



#### index.js

这里 把 axios 注册 为 Vue 插件 使用， 并将 api 模块 挂 载在 Vue 原型 的$ api 对象 上。 这样 在 能 获取 this 引用 的 地方 就可以 通过“ this.$ api. 子 模块. 方法” 的 方式 调用 API 了。

~~~js
import api from '@/http/api'

const install = Vue => {
  if (install.installed) {
    return
  }
  install.installed = true
  Object.defineProperties(Vue.prototype, {
    //注意，此处挂载在Vue原型的$api对象上
    $api: {
      get() {
        return api
      }
    }
  })
}

export default install

~~~



#### api.js

此 模块 是一 个 聚合 模块， 汇合 modules 目 录下 的 所有 子 模块 API。

~~~js
//接口统一集成模块
import * as login from '@/http/modules/login'
import * as user from '@/http/modules/user'

//默认全部导出
export default {
  login,
  user
}

~~~

### 注意事项：

- params是添加到url的请求字符串中的，用于`get/delete/patch/put`请求。
- data是添加到请求体（body）中的， 用于`post`请求。

#### user.js

modules 目 录下 的 子 模块 太多， 不方便 全 贴， 这里 就以 用户 管理 模块 为例。



~~~js
import axios from '@/http/axios'

/**
 * 用户管理模块
 */

export function add(data) {
  return axios({
    url: '/users',
    method: 'post',
    data
  })
}

export function remove(data) {
  return axios({
    url: '/users',
    method: 'delete',
    params： data
  })
}

export function update(data) {
  return axios({
    url: '/users',
    method: 'put',
    data
  })
}

export function getList(data) {
  return axios({
    url: '/users',
    method: 'get',
    params: data
  })
}

~~~





#### login.js

~~~js
import axios from '@/http/axios'

/**
 * 用户登录模块
 */
export const login = data => {
  return axios({
    url: '/login',
    method: 'post',
    data
  })
}

export const getInfo = data => {
  return axios({
    url: '/login',
    method: 'get',
    params: data
  })
}

~~~



#### main.js

修改 main. js， 导入 API 模块， 并 通过 Vue. use( api) 语句 进行 使用 注册， 这样 就可以 通过“ `this.$ api.子模块.方法`” 的 方式 来 调用 后台 接口 了。 

引入 global 模块， 并 通过 Vue. prototype. global = global 语句 进行 挂 载， 这样 就可以 通过 `this.gloabl.xx` 来 获取 全局 配置 了。

~~~bash
import Vue from "vue";
import App from "@/App.vue";
import router from "@/router";
import * as api from "@/http";
import store from "@/store";
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";

// Vue.config.productionTip = false;

Vue.use(ElementUI);
Vue.use(api);

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount("#app");

~~~



### 登录流程测试

> 主要逻辑

调用后台登录接口，然后跳转到主页

修改login.vue来测试

~~~vue
<template>
  <div class="login_container">
    <div class="box">
      <!-- LOG区域 -->
      <div class="logo_name">
        ELITE
      </div>

      <!-- 标题区域 -->
      <div class="title_box">
        <h3>欢迎来到ELITE</h3>
        <p>登录后，查看更多</p>
      </div>

      <!-- 登录区域 -->
      <div class="login_box">
        <el-form :model="loginForm"
                 :rules="loginFormRules"
                 ref="loginFormRef"
                 label-width="0px">
          <!-- 用户名 -->
          <el-form-item prop="username">
            <el-input v-model="loginForm.username"
                      prefix-icon="fa fa-user"
                      clearable
                      @keyup.enter.native="login">
            </el-input>
          </el-form-item>

          <!-- 密码 -->
          <el-form-item prop="password">
            <el-input v-model="loginForm.password"
                      prefix-icon="fa fa-lock"
                      type="password"
                      show-password
                      clearable
                      @keyup.enter.native="login">
            </el-input>
          </el-form-item>

          <!-- 按钮区域 -->
          <el-form-item>
            <el-button @click="login"
                       type="success"
                       v-loading.fullscreen.lock="fullscreenLoading"
                       round>
              登录
            </el-button>
          </el-form-item>
          <!-- <p class="no_account_tips"><small>还没有账号?</small></p>
          <el-button round>注册</el-button> -->
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
import { setToken } from '@/utils/auth'
export default {
  data () {
    return {
      // 登录表单的数据绑定对象
      loginForm: {
        username: '',
        password: ''
      },
      // 登录表单的验证规则对象
      loginFormRules: {
        // 验证用户名是否合法
        username: [
          { required: true, message: '请输入账号', trigger: 'blur' },
          { min: 4, max: 15, message: '长度在 4 到 15 个字符', trigger: 'blur' }
        ],
        // 验证密码是否合法
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      },
      // 控制loading组件
      fullscreenLoading: false
    }
  },
  methods: {
    // 登录方法
    login () {
      this.loading = true
      this.$refs.loginFormRef.validate(valid => {
        if (!valid) {
          return this.$notify.warning({
            title: '请输入账号和密码！',
            message: '登录失败！'
          })
        }
        this.$api.login.login(this.loginForm).then((res) => {
          if (res.code === 403) {
            return this.$notify.warning({
              title: res.data,
              message: '登录失败！权限不足！'
            })
          }
          if (res.code !== 200) {
            this.fullscreenLoading = false
            return this.$notify.error({
              title: res.message,
              message: '登录失败！'
            })
          }
          this.$notify.success({
            title: res.message,
            message: '登录成功！'
          })
          // 放置token到Cookie
          setToken(res.data.token)
          // 登录成功，跳转到主页
          this.$router.push('/home')
        }).catch((res) => {
          this.$message({
            message: res.message,
            type: 'error'
          })
        })
        this.loading = false
      })
    }
  },
  watch: {
    $route (to, from) {
      // 以服务的方式调用的 Loading 需要异步关闭
      this.$nextTick(() => {
      })
    }
  }
}
</script>

<style lang="less" scoped>
.input {
  font-size: 0.9rem;
}

.el-form {
  position: absolute;
  bottom: 0;
  width: 70%;
  padding: 0 20px;
  box-sizing: border-box;
  margin: 0 auto;
  left: 50%;
  transform: translate(-50%, 0);
}

.no_account_tips {
  text-align: center;
}

.el-button {
  width: 100%;
}

.title_box {
  text-align: center;
  font-family: 'open sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 13px;
  p {
    font-size: 13px;
    color: #676a6c;
  }
}

h3 {
  font-weight: 600;
  font-size: 16px;
  color: #676a6c;
}

.box {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.logo_name {
  color: #e6e6e6;
  font-size: 180px;
  font-weight: 800;
  letter-spacing: -10px;
  text-align: center;
  font-family: none;
}

.login_box {
  height: 220px;
  border-radius: 3px;
}

.login_container {
  background-color: #f3f3f4;
  height: 100%;
}
</style>

~~~



 

测试成功

![image-20200719011841251](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233403-812222.png)

![image-20200719011857463](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233405-400468.png)





## 使用Font Awesome第三方图标库

因为Element-ui的图标不够丰富，我这里选择第三方图标库

> 官网
>
> http://fontawesome.dashgame.com/。



### 安装依赖

~~~bash
yarn add font-awesome
~~~

### 导入项目

在main.js中引入

~~~js
import 'font-awesome/css/font-awesome.min.css'
~~~

### 测试

随便在home.vue中测试

~~~html
<li class="fa fa-home fa-lg"></li>
~~~

测试结果:

![image-20200717181026557](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233408-116225.png)



有小房子图标,说明引入成功.



## 多语言国际化

### 安装依赖

~~~bash
yarn add vue-i18n
~~~



### 添加配置

在`src`新建`i18n`目录，并新建`index.js`

~~~js
import Vue from 'vue'
import VueI18n from 'vue-i18n'

Vue.use(VueI18n)

// 注册i18n实例并引入语言文件
const i18n = new VueI18n({
  locale: 'zh_cn',
  messages: {
    zh_cn: require('@/assets/languages/zh_CN.json'),
    en_us: require('@/assets/languages/en_us.json'),
    es_ve: require('@/assets/languages/es-ve.json')
  }
})

export default i18n

~~~

在src下新建asses文件夹，新建languages文件夹，分别新建`zh_cn.json`、`en_us.json`和`es_ve.json`



#### `zh_cn.json`

~~~json
{
  "common":{
    "home":"首页",
    "login":"登录",
    "logout":"退出登录",
    "doc":"文档",
    "blog":"博客"
  }
}
~~~

#### `en_us.json`

~~~json
{
  "common":{
    "home":"home",
    "login":"login",
    "logout":"logout",
    "doc":"doc",
    "blog":"blog"
  }
}
~~~

#### 在 main. js 中 引入 i18n 并 注入 vue 对象 中。

> main.js

~~~js
import Vue from 'vue'
import App from '@/App.vue'
import VueRouter from 'vue-router'
import router from '@/router'
import api from '@/http'
import i18n from '@/i18n'
import global from '@/utils/global'
import Element from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import 'font-awesome/css/font-awesome.min.css'

Vue.use(VueRouter)
Vue.use(Element) // 注册使用Element
Vue.use(api) // 注册API模块

Vue.prototype.global = global // 挂载全局配置模块

new Vue({
  i18n,
  router,
  render: h => h(App)
}).$mount('#app')

~~~





### 测试

在测试页面

~~~vue
<!-- 测试i18n -->
    <div>
      <h3>{{$t('common.doc')}}</h3>
      <h3>{{$t('common.login')}}</h3>
      <h3>{{$t('common.logout')}}</h3>
      <div>
        <el-button type="success" @click="changeLanguage('zh_cn')">简体中文</el-button>
        <el-button type="success" @click="changeLanguage('en_us')">English</el-button>
        <el-button type="success" @click="changeLanguage('es_ve')">Español</el-button>
      </div>
    </div>
~~~

> script

~~~js
  changeLanguage(type) {
      if (!type) {
        type = 'zh_cn'
      }
      console.log('type:  ' + type)
      this.$i18n.locale = type
      this.langVisible = false
    }
~~~



测试结果：

![image-20200719003704972](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233411-280679.png)

![image-20200719003714346](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233413-659445.png)

![image-20200719003725168](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233416-612914.png)

通过 `this.$i18n.locale = xx` 方式 就可以 全局 切换 语言， Vue 框架 会 根据 locale 的 值 读取 对应 的 国际化 多语 言 文件 并进 行 适时 更新。



### 那么在js中如何调用？

~~~js
this.$t('xx')
~~~





## 主页面Layout

### 页面设计

![image-20200719011954251](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233419-769417.png)



### Home.vue

~~~vue
<template>
  <div class="home-container">
    <el-container>
      <!-- 侧边区域 -->
      <nav-bar class="test"></nav-bar>

      <!-- 页面主体区域 -->
      <el-container>
        <!-- 右侧头部区域 -->
        <el-header>
          <head-bar></head-bar>
        </el-header>

        <!-- 右侧内容区域 -->
        <el-main>
          <main-content></main-content>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import NavBar from '@/views/layout/navBar'
import HeadBar from '@/views/layout/headBar'
import MainContent from '@/views/layout/mainContent'

export default {
  components: {
    NavBar,
    HeadBar,
    MainContent
  }
}
</script>

<style lang="scss" scoped>
.el-main {
  background-color: rgb(243, 243, 244);
  height: 100%;
}

.test {
  background-color: rgb(243, 243, 244);
}

.home-container {
  height: 100%;
}

.el-container {
  height: 100%;
}
</style>

~~~



> src下新建layout文件夹，并且新建headBar.vue，mainContent，navBar.vue



### headBar.vue

头部导航主要是设置样式，并在右侧添加用户名和头像显示。

~~~vue
<template>
  <div class="headbar" style="background:#14889A" :class="'position-left'">
    <!-- 工具栏 -->
    <span class="toolbar">
      <el-menu class="el-menu-demo" background-color="#14889A" text-color="#14889A" active-text-color="#14889A" mode="horizontal">
        <el-menu-item index="1">
          <!-- 用户信息 -->
          <span class="user-info"><img :src="user.avatar" />{{user.name}}</span>
        </el-menu-item>
      </el-menu>
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        name: 'Saul.J.Wu',
        avatar: '',
        role: '超级管理员',
        registeInfo: '注册时间：2018-12-20 '
      }
    }
  },
  methods: {

  }
}
</script>

<style scoped lang="scss">
.headbar {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 1030;
  height: 60px;
  line-height: 60px;
  border-color: rgba(180, 190, 190, 0.8);
  border-left-width: 1px;
  border-left-style: solid;
}
.navbar {
  float: left;
}
.toolbar {
  float: right;
}
.user-info {
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  img {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    margin: 10px 0px 10px 10px;
    float: right;
  }
}
.position-left {
  left: 200px;
}
</style>

~~~



### navBar.vue

~~~vue
<template>
  <div class="menu-bar-container">
    <!-- logo -->
    <div class="logo" style="background:#14889A" :class="'menu-bar-width'"
        @click="$router.push('/')">
        <img src="@/assets/logo.png"/> <div>Mango</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  methods: {

  },
  components: {

  }
}

</script>

<style lang='scss'>
.menu-bar-container {
  position: fixed;
  top: 0px;
  left: 0;
  bottom: 0;
  z-index: 1020;
  .logo {
    position:absolute;
    top: 0px;
    height: 60px;
    line-height: 60px;
    background: #545c64;
    cursor:pointer;
    img {
        width: 40px;
        height: 40px;
        border-radius: 0px;
        margin: 10px 10px 10px 10px;
        float: left;
    }
    div {
      font-size: 25px;
      color: white;
      text-align: left;
      padding-left: 20px;
    }
  }
  .menu-bar-width {
    width: 200px;
  }
}

</style>

~~~



### mainContent.vue

主要内容区域包含标签页导航和主内容区域，在主内容中防止`route-view`，用于路由信息。

~~~vue
<template>
   <div id="main-container" class="main-container" :class="'position-left'">
    <!-- 标签页 -->
    <div class="tab-container"></div>
    <!-- 主内容区域 -->
    <div class="main-content">
      <keep-alive>
        <transition name="fade" mode="out-in">
            <router-view></router-view>
        </transition>
      </keep-alive>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  methods: {

  },
  components: {

  }
}

</script>

<style lang='scss'>
.main-container {
  padding: 0 5px 5px;
  position: absolute;
  top: 60px;
  left: 1px;
  right: 1px;
  bottom: 0px;
  background: rgba(67, 69, 70, 0.1);
  .main-content {
    position: absolute;
    top: 45px;
    left: 5px;
    right: 5px;
    bottom: 5px;
    padding: 5px;
  }
}
.position-left {
  left: 200px;
}
</style>

~~~

### 测试结果

![image-20200719014154048](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233426-858645.png)



## 管理应用状态vuex

> 在很多应用场景下，我们需要在组件之间共享状态。

比如我们的左侧导航栏需要收缩和展开的功能，收缩状态时宽度很小，只显示菜单图标，因为导航菜单栏收缩之后宽度变了，所以右侧的主内容区域要占用导航栏收缩的空间，主内容区域宽度也要根据导航栏的收缩状态做变更，而导航栏和主内容区域是两个不同的组件，而非父子组件之间不支持状态传递，所以组件之间的状态共享问题发生了。

vuex是一个专为vue.js应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。本章将通过实现左侧导航栏的收缩展开功能来讲解怎样使用vuex来管理应用状态。

> 更多vuex的资料可参考：https://vuex.vuejs.org/zh/。

### 安装依赖

~~~bash
yarn add vuex
~~~

### 添加Store

在src目录下新建一个store目录，专门管理应用状态。

![image-20200719014733822](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233429-58464.png)



#### index.js

在index.js中引入vuex并统一组织导入和管理子模块。

~~~js
import Vue from 'vue'
import Vuex from 'vuex'

//引入子模块
import app from '@/store/modules/app'

Vue.use(Vuex)

const store = new Vuex.Store({
  modules: {
    app: app
  }
})

export default store

~~~



#### app.js

app.js是属于应用内的全局性的配置，比如主题色、导航栏收缩状态等，详情见注释

~~~js
const app = {
  state: {
    appName: 'Elite', // 应用名称
    themeColor: '#24292e', // 主题颜色
    oldThemeColor: '#24292e', // 上一次主题颜色
    collapse: false // 导航栏收缩状态
  },
  getters: {
    // 对应着上面state
    collapse: state => state.collapse
  },
  mutations: {
    // 改变收缩状态
    CHANGE_COLLAPSE(state) {
      state.collapse = !state.collapse
    },
    // 改变主题颜色
    SET_THEME_COLOR(state, themeColor) {
      state.oldThemeColor = state.themeColor
      state.themeColor = themeColor
    }
  },
  actions: {
    collapseAsync({ commit }) {
      commit('CHANGE_COLLAPSE')
    },
    themeColorAsync({ commit }, newColor) {
      commit('SET_THEME_COLOR', newColor)
    }
  }
}

export default app

~~~

### 引入Store

在main.js中引入Store

![image-20200719015837774](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233433-161523.png)





~~~js
import Vue from 'vue'
import App from '@/App.vue'
// import VueRouter from 'vue-router'
import router from '@/router'
import api from '@/http'
import i18n from '@/i18n'
import store from '@/store'
import global from '@/utils/global'
import Element from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import 'font-awesome/css/font-awesome.min.css'

// Vue.use(VueRouter)
Vue.use(Element) // 注册使用Element
Vue.use(api) // 注册API模块

Vue.prototype.global = global // 挂载全局配置模块

new Vue({
  i18n,
  router,
  store,
  render: h => h(App)
}).$mount('#app')

~~~



### 使用Store

这里以头部页面HeadBarvue的状态使用为例，其他页面同理，详见代码。

首先通过computed计算属性引入store属性，这样就可以直接在页面中通过collapse引用状态值了。

当然如果不嫌长，也可以不使用计算属性，直接在页面中通过`$store.state.app.collapse`引用。

例如下面关键代码：

~~~vue
<template>
  <div style="background:#14889A" :class="collapse?'position-collapse-left':'position-left'">
    <!-- 工具栏 -->
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState({
      collapse: state => state.app.collapse
    })
  }
}
</script>


<style scoped lang="scss">

.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}
</style>
~~~



### 收缩组件

在src下新建components/Hamburger目录，并创建导航栏收缩展开组件index.vue。

> 组件是使用SVG绘制，绘制根据isActive状态是否旋转，显示收缩和展开不同的图形

#### Hamburger

~~~vue
<template>
  <svg
    t="1492500959545"
    @click="onCollapse"
    class="hamburger"
    fill="#fff"
    fill-opacity="0.8"
    :class="{ 'is-active': collapse }"
    viewBox="0 0 1024 1024"
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    p-id="1691"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    width="64"
    height="64"
  >
    <path
      d="M966.8023 568.849776 57.196677 568.849776c-31.397081 0-56.850799-25.452695-56.850799-56.850799l0 0c0-31.397081 25.452695-56.849776 56.850799-56.849776l909.605623 0c31.397081 0 56.849776 25.452695 56.849776 56.849776l0 0C1023.653099 543.397081 998.200404 568.849776 966.8023 568.849776z"
      p-id="1692"
    ></path>
    <path
      d="M966.8023 881.527125 57.196677 881.527125c-31.397081 0-56.850799-25.452695-56.850799-56.849776l0 0c0-31.397081 25.452695-56.849776 56.850799-56.849776l909.605623 0c31.397081 0 56.849776 25.452695 56.849776 56.849776l0 0C1023.653099 856.07443 998.200404 881.527125 966.8023 881.527125z"
      p-id="1693"
    ></path>
    <path
      d="M966.8023 256.17345 57.196677 256.17345c-31.397081 0-56.850799-25.452695-56.850799-56.849776l0 0c0-31.397081 25.452695-56.850799 56.850799-56.850799l909.605623 0c31.397081 0 56.849776 25.452695 56.849776 56.850799l0 0C1023.653099 230.720755 998.200404 256.17345 966.8023 256.17345z"
      p-id="1694"
    ></path>
  </svg>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'hamburger',
  methods: {
    // 折叠导航栏
    onCollapse: function() {
      this.$store.dispatch('collapseAsync')
    }
  },
  computed: {
    ...mapState({
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style scoped>
.hamburger {
  display: inline-block;
  cursor: pointer;
  width: 20px;
  height: 20px;
  transform: rotate(0deg);
  transition: 0.38s;
  transform-origin: 50% 50%;
}
.hamburger.is-active {
  transform: rotate(90deg);
}
</style>

~~~



> 在头部区域headBar中引入hamburger，并将自身isActive状态跟收缩状态collapse绑定。
>
> 并添加单机导航栏收缩组件区域的响应函数，设置导航收缩状态到Store。

#### headBar.vue

~~~vue
<template>
  <div
    style="background:#14889A"
    :class="[collapse ? 'position-collapse-left' : 'position-left', 'headbar']"
  >
    <!-- 导航收缩 -->
    <span class="hamburg">
      <el-menu
        class="el-menu-demo"
        background-color="#14889A"
        text-color="#fff"
        active-text-color="#14889A"
        mode="horizontal"
      >
        <el-menu-item index="1">
          <hamburger></hamburger>
        </el-menu-item>
      </el-menu>
    </span>

    <!-- 工具栏 -->
    <span class="toolbar">
      <el-menu
        class="el-menu-demo"
        background-color="#14889A"
        text-color="#14889A"
        active-text-color="#14889A"
        mode="horizontal"
      >
        <el-menu-item index="1">
          <!-- 用户信息 -->
          <span class="user-info"
            ><img :src="user.avatar" />{{ user.name }}</span
          >
        </el-menu-item>
      </el-menu>
    </span>

    <!-- 头部右边区域 -->
    <!-- <span class="top-right">
      <el-button type="info">退出</el-button>
    </span> -->
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Hamburger from '@/components/Hamburger/index'
export default {
  components: {
    Hamburger
  },
  data() {
    return {
      user: {
        name: 'Saul.J.Wu',
        avatar: 'https://s1.ax1x.com/2020/07/19/URgwyn.jpg',
        role: '超级管理员',
        registeInfo: '注册时间：2018-12-20 '
      }
    }
  },
  methods: {},
  computed: {
    ...mapState({
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style lang="scss" scoped>
.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}

.headbar {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 1030;
  height: 60px;
  line-height: 60px;
  border-color: rgba(180, 190, 190, 0.8);
  border-left-width: 1px;
  border-left-style: solid;
}

.user-info {
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  img {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    margin: 10px 0px 10px 10px;
    float: right;
  }
}

.navbar {
  float: left;
}
.hamburg,
.navbar {
  float: left;
}
.toolbar {
  float: right;
}
</style>

~~~



#### navbar.vue也要修改

~~~vue
<template>
  <div
    :class="[
      collapse ? 'menu-bar-collapse-width' : 'menu-bar-width',
      'menu-bar-container'
    ]"
  >
    <!-- logo -->
    <div
      @click="$router.push('/')"
      class="logo"
      :style="{ background: themeColor }"
      :class="collapse ? 'menu-bar-collapse-width' : 'menu-bar-width'"
    >
      <img src="@/assets/logo.png" />
      <div>{{ collapse ? '' : appName }}</div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {}
  },
  methods: {},
  components: {},
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse,
      appName: state => state.app.appName
    })
  }
}
</script>

<style lang="scss" scoped>
.el-menu {
  position: absolute;
  top: 60px;
  bottom: 0px;
  text-align: left;
  // background-color: #2968a30c;
}

.menu-bar-container {
  position: fixed;
  top: 0px;
  left: 0;
  bottom: 0;
  z-index: 1020;
  .logo {
    height: 60px;
    line-height: 60px;
    background: #545c64;
    cursor: pointer;
    img {
      width: 40px;
      height: 40px;
      border-radius: 0px;
      margin: 10px 10px 10px 10px;
      float: left;
    }
    div {
      font-size: 25px;
      color: white;
      text-align: left;
      padding-left: 20px;
    }
  }
}
.menu-bar-width {
  width: 200px;
}
.menu-bar-collapse-width {
  width: 65px;
}
</style>

~~~





### 页面测试

启动应用

~~~bash
yarn serve
~~~

访问主页

![image-20200719031754754](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233444-51643.png)

当我点击时

![image-20200719031806775](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233447-511333.png)





## 头部功能组件

现在为头部区域一些常用功能的实现方案，比如动态主题切换器、国际化语言切换器、用户信息弹出面板等。



### 主题切换组件

> 实现思路

使用一个颜色选取组件elcolorpicker获取一个主题色，然后通过动态替换覆盖Element默认CSS样式的方式替换框架的主题色primarycolor，并在主题色切换成功之后提供回调函数，通过此回调函数同步更新需要更换为主题色的页面或组件。

通过watch监听theme属性即主题色的更新动态替换CSS样式，修改主题色，并在替换CSS之后通过`this.$emit('onThemeChange',val)`语句提供一个回调函数'onThemeChange'并将更新后的主题色的值val作为参数传入，使得外部组件可以通过此回调函数同步更新外部组件颜色。



#### 编写组件

在src/components下，新建themePicker目录，新建index.vue

~~~vue
<template>
  <el-color-picker class="theme-picker" popper-class="theme-picker-dropdown"
    v-model="theme" :size="size" @change="onThemeChange">
  </el-color-picker>
</template>

<script>

const version = require('element-ui/package.json').version // element-ui
const ORIGINAL_THEME = '#409EFF' // default color

export default {
  name: 'ThemePicker',
  props: {
    default: { // 初始化主题，可由外部传入
      type: String,
      default: null
    },
    size: { // 初始化主题，可由外部传入
      type: String,
      default: 'small'
    }
  },
  data() {
    return {
      chalk: '', // content of theme-chalk css
      theme: ORIGINAL_THEME,
      showSuccess: true // 是否弹出换肤成功消息
    }
  },
  mounted() {
    if (this.default != null) {
      this.theme = this.default
      this.$emit('onThemeChange', this.theme)
      this.showSuccess = false
    }
  },
  watch: {
    theme(val, oldVal) {
      if (typeof val !== 'string') return
      // 替换CSS样式，修改主题色
      const themeCluster = this.getThemeCluster(val.replace('#', ''))
      const originalCluster = this.getThemeCluster(oldVal.replace('#', ''))
      const getHandler = (variable, id) => {
        return () => {
          const originalCluster = this.getThemeCluster(ORIGINAL_THEME.replace('#', ''))
          const newStyle = this.updateStyle(this[variable], originalCluster, themeCluster)

          let styleTag = document.getElementById(id)
          if (!styleTag) {
            styleTag = document.createElement('style')
            styleTag.setAttribute('id', id)
            document.head.appendChild(styleTag)
          }
          styleTag.innerText = newStyle
        }
      }
      const chalkHandler = getHandler('chalk', 'chalk-style')
      if (!this.chalk) {
        const url = `https://unpkg.com/element-ui@${version}/lib/theme-chalk/index.css`
        this.getCSSString(url, chalkHandler, 'chalk')
      } else {
        chalkHandler()
      }
      const styles = [].slice.call(document.querySelectorAll('style'))
        .filter(style => {
          const text = style.innerText
          return new RegExp(oldVal, 'i').test(text) && !/Chalk Variables/.test(text)
        })
      styles.forEach(style => {
        const { innerText } = style
        if (typeof innerText !== 'string') return
        style.innerText = this.updateStyle(innerText, originalCluster, themeCluster)
      })
      // 响应外部操作
      this.$emit('onThemeChange', val)
      if (this.showSuccess) {
        this.$message({ message: '换肤成功', type: 'success' })
      } else {
        this.showSuccess = true
      }
    }
  },
  methods: {
    updateStyle(style, oldCluster, newCluster) {
      let newStyle = style
      oldCluster.forEach((color, index) => {
        newStyle = newStyle.replace(new RegExp(color, 'ig'), newCluster[index])
      })
      return newStyle
    },

    getCSSString(url, callback, variable) {
      const xhr = new XMLHttpRequest()
      xhr.onreadystatechange = () => {
        if (xhr.readyState === 4 && xhr.status === 200) {
          this[variable] = xhr.responseText.replace(/@font-face{[^}]+}/, '')
          callback()
        }
      }
      xhr.open('GET', url)
      xhr.send()
    },

    getThemeCluster(theme) {
      const tintColor = (color, tint) => {
        let red = parseInt(color.slice(0, 2), 16)
        let green = parseInt(color.slice(2, 4), 16)
        let blue = parseInt(color.slice(4, 6), 16)

        if (tint === 0) { // when primary color is in its rgb space
          return [red, green, blue].join(',')
        } else {
          red += Math.round(tint * (255 - red))
          green += Math.round(tint * (255 - green))
          blue += Math.round(tint * (255 - blue))

          red = red.toString(16)
          green = green.toString(16)
          blue = blue.toString(16)

          return `#${red}${green}${blue}`
        }
      }

      const shadeColor = (color, shade) => {
        let red = parseInt(color.slice(0, 2), 16)
        let green = parseInt(color.slice(2, 4), 16)
        let blue = parseInt(color.slice(4, 6), 16)

        red = Math.round((1 - shade) * red)
        green = Math.round((1 - shade) * green)
        blue = Math.round((1 - shade) * blue)

        red = red.toString(16)
        green = green.toString(16)
        blue = blue.toString(16)

        return `#${red}${green}${blue}`
      }

      const clusters = [theme]
      for (let i = 0; i <= 9; i++) {
        clusters.push(tintColor(theme, Number((i / 10).toFixed(2))))
      }
      clusters.push(shadeColor(theme, 0.1))
      return clusters
    },

    // 切换主题
    onThemeChange: function(themeColor) {
      this.$store.commit('setThemeColor', themeColor)
    }
  }
}
</script>

<style scoped>
.theme-picker .el-color-picker__trigger {
  vertical-align: middle;
}

.theme-picker-dropdown .el-color-dropdown__link-btn {
  display: none;
}
</style>

~~~



#### 引入组件

在headBar.vue引入主题切换组件

~~~js
import ThemePicker from '@/components/themePicker'
components: {
    ThemePicker
  }
~~~



关键代码在涉及的地方引入。

`:style="{'background':themeColor}"`

`:background-color="themeColor"`

 ` :active-text-color="themeColor"`



同时

![image-20200719033905600](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233452-639116.png)

#### headBar.vue

~~~vue
<template>
  <div
    :style="{ background: themeColor }"
    :class="[collapse ? 'position-collapse-left' : 'position-left', 'headbar']"
  >
    <!-- 导航收缩 -->
    <span class="hamburg">
      <hamburger></hamburger>
    </span>

    <!-- 工具栏 -->
    <span class="toolbar">
      <el-menu
        class="el-menu-demo"
        :background-color="themeColor"
        :active-text-color="themeColor"
        text-color="#14889A"
        mode="horizontal"
      >
        <!-- 主题切换 -->
        <el-menu-item index="1">
          <theme-picker class="theme-picker" :default="themeColor">
          </theme-picker>
        </el-menu-item>

        <!-- 用户信息 -->
        <el-menu-item index="2">
          <span class="user-info"
            ><img :src="user.avatar" />{{ user.name }}</span
          >
        </el-menu-item>
        <!-- 头部右边区域 -->
        <!-- <span class="top-right">
      <el-button type="info">退出</el-button>
    </span> -->
      </el-menu>
    </span>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Hamburger from '@/components/Hamburger'
import ThemePicker from '@/components/ThemePicker'
export default {
  components: {
    Hamburger,
    ThemePicker
  },
  data() {
    return {
      user: {
        name: 'Saul.J.Wu',
        avatar: 'https://s1.ax1x.com/2020/07/19/URgwyn.jpg',
        role: '超级管理员',
        registeInfo: '注册时间：2018-12-20 '
      }
    }
  },
  methods: {},
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style lang="scss" scoped>
.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}

.headbar {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 1030;
  height: 60px;
  line-height: 60px;
  border-color: rgba(180, 190, 190, 0.8);
  border-left-width: 1px;
  border-left-style: solid;
}

.user-info {
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  img {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    margin: 10px 0px 10px 10px;
    float: right;
  }
}

.navbar {
  float: left;
}
.hamburg,
.navbar {
  float: left;
}
.toolbar {
  float: right;
}
</style>

~~~



#### navBar.vue

~~~vue
<template>
  <div
    :class="[
      collapse ? 'menu-bar-collapse-width' : 'menu-bar-width',
      'menu-bar-container'
    ]"
  >
    <!-- logo -->
    <div
      @click="$router.push('/')"
      class="logo"
      :style="{ background: themeColor }"
      :class="collapse ? 'menu-bar-collapse-width' : 'menu-bar-width'"
    >
      <img src="@/assets/logo.png" />
      <div>{{ collapse ? '' : appName }}</div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {}
  },
  methods: {},
  components: {},
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse,
      appName: state => state.app.appName
    })
  }
}
</script>

<style lang="scss" scoped>
.el-menu {
  position: absolute;
  top: 60px;
  bottom: 0px;
  text-align: left;
  // background-color: #2968a30c;
}

.menu-bar-container {
  position: fixed;
  top: 0px;
  left: 0;
  bottom: 0;
  z-index: 1020;
  .logo {
    height: 60px;
    line-height: 60px;
    background: #545c64;
    cursor: pointer;
    img {
      width: 40px;
      height: 40px;
      border-radius: 0px;
      margin: 10px 10px 10px 10px;
      float: left;
    }
    div {
      font-size: 25px;
      color: white;
      text-align: left;
      padding-left: 20px;
    }
  }
}
.menu-bar-width {
  width: 200px;
}
.menu-bar-collapse-width {
  width: 65px;
}
</style>

~~~

#### 测试

![image-20200719034257825](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233458-849968.png)



![image-20200719034305151](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233501-722732.png)





### 语言切换组件

实现效果：在headBar.vue工具栏主题切换器右边放置一个语言切换组件。

#### 编写组件

在src/components下，新建LanguageSelect目录，新建index.vue

~~~vue
<template>
  <div>
    <el-dropdown v-if="cssType === 'dropdown'" @command="changeLanguage" trigger="click">
      <el-button type="primary">
        <i class="fa fa-language fa-lg" style="color:#FFF"></i>
      </el-button>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item command="zh_cn">简体中文</el-dropdown-item>
        <el-dropdown-item command="en_us">English</el-dropdown-item>
        <el-dropdown-item command="es_ve">Español</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>

    <el-radio-group v-if="cssType === 'radio'" v-model="radio" @change="changeLanguage">
      <el-radio label="zh_cn">简体中文</el-radio>
      <el-radio label="en_us">English</el-radio>
      <el-radio label="es_ve">Español</el-radio>
    </el-radio-group>
  </div>
</template>

<script>
export default {
  name: 'language-select',
  props: {
    cssType: {
      type: String,
      default: 'dropdown'
    }

  },
  data() {
    return {
      radio: 'zh_cn'
    }
  },
  methods: {
    // 语言切换
    changeLanguage(lang) {
      if (!lang) {
        lang = 'zh_cn'
      }
      this.$i18n.locale = lang
      this.langVisible = false
    }
  }
}
</script>

~~~



#### 引入组件

在headBar中引入

![image-20200719042937336](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233505-610292.png)



![image-20200719043009117](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233507-469666.png)



headBar.vue完整代码

~~~vue
<template>
  <div
    :style="{ background: themeColor }"
    :class="[collapse ? 'position-collapse-left' : 'position-left', 'headbar']"
  >
    <!-- 导航收缩 -->
    <span class="hamburg">
      <hamburger></hamburger>
    </span>

    <!-- 测试语言选择组件 -->
    <span style="color:#fff">
      <span>
        {{ $t('common.home') }}
      </span>
      <span>
        {{ $t('common.doc') }}
      </span>
      <span>
        {{ $t('common.blog') }}
      </span>
    </span>

    <!-- 工具栏 -->
    <span class="toolbar">
      <el-menu
        class="el-menu-demo"
        :background-color="themeColor"
        :active-text-color="themeColor"
        text-color="#14889A"
        mode="horizontal"
      >
        <!-- 主题切换 -->
        <el-menu-item index="1">
          <theme-picker class="theme-picker" :default="themeColor">
          </theme-picker>
        </el-menu-item>

        <!-- 语言切换 -->
        <el-menu-item index="2">
          <language-select></language-select>
        </el-menu-item>

        <!-- 用户信息 -->
        <el-menu-item index="3">
          <span class="user-info"
            ><img :src="user.avatar" />{{ user.name }}</span
          >
        </el-menu-item>
        <!-- 头部右边区域 -->
        <!-- <span class="top-right">
      <el-button type="info">退出</el-button>
    </span> -->
      </el-menu>
    </span>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Hamburger from '@/components/Hamburger'
import ThemePicker from '@/components/ThemePicker'
import LanguageSelect from '@/components/LanguageSelect'
export default {
  components: {
    Hamburger,
    ThemePicker,
    LanguageSelect
  },
  data() {
    return {
      user: {
        name: 'Saul.J.Wu',
        avatar: 'https://s1.ax1x.com/2020/07/19/URgwyn.jpg',
        role: '超级管理员',
        registeInfo: '注册时间：2018-12-20 '
      }
    }
  },
  methods: {},
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style lang="scss" scoped>
.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}

.headbar {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 1030;
  height: 60px;
  line-height: 60px;
  border-color: rgba(180, 190, 190, 0.8);
  border-left-width: 1px;
  border-left-style: solid;
}

.user-info {
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  img {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    margin: 10px 0px 10px 10px;
    float: right;
  }
}

.navbar {
  float: left;
}
.hamburg,
.navbar {
  float: left;
}
.toolbar {
  float: right;
}
</style>

~~~



#### 测试结果

![image-20200719044527124](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233512-772142.png)



![image-20200719044535160](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233515-351375.png)



![image-20200719044540332](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233517-145201.png)



那么我们要一个个地填key value吗？有没有更方便的方法？有



## vscode的i18n Ally插件

### 安装插件

![image-20200719070114917](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233614-69211.png)

### 配置插件

先修改json文件名称，不然检测不到，![image-20200719070250858](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233615-196307.png)



`CTRL+P`，搜索`i18n`更新默认显示为中文



### 如何使用？

选中要的文件CTRL+P搜索i18n提取文案，然后去到UI界面，点击翻译。



## 完善登陆页面

因为用户信息需要保存起来，所以还要管理应用状态vuex

### user.js

> 路径：src/store/modules/user.js

~~~js
import router from '@/router'
import { getToken, setToken, removeToken } from '@/utils/auth'
import { login } from '@/http/modules/login'
import { Message } from 'element-ui'

const user = {
  state: {
    token: getToken(),
    name: '',
    avatar: '',
    role: '',
    createTime: '',
    prevLoginTime: ''
  },
  mutations: {
    SET_TOKEN: (state, token) => {
      state.token = token
    },
    SET_NAME: (state, name) => {
      state.name = name
    },
    SET_AVATAR: (state, avatar) => {
      state.avatar = avatar
    },
    SET_ROLE: (state, role) => {
      state.role = role
    },
    SET_CREATE_TIME: (state, createTime) => {
      state.createTime = createTime
    },
    SET_PREV_LOGIN_TIME: (state, prevLoginTime) => {
      state.prevLoginTime = prevLoginTime
    },
    SET_USER_INFO(state, userInfo) {
      state.name = user.username
      state.avatar = user.icon
      state.role = user.note
      state.createTime = user.createTime
      state.prevLoginTime = user.loginTime
    }
  },

  actions: {
    // 登录同步
    Login({ commit }, loginParam) {
      loginParam.username = loginParam.username.trim()
      return new Promise((resolve, reject) => {
        login(loginParam)
          .then(res => {
            if (res.code === 403) {
              Message.warning(res.message)
              return reject(res.message)
            }
            if (res.code !== 200) {
              this.fullscreenLoading = false
              Message.error(res.message)
              return reject(res.message)
            }
            Message.success(res.message)
            const tokenStr = res.data.tokenHead + res.data.token
            setToken(tokenStr)
            commit('SET_TOKEN', tokenStr)
            commit('SET_USER_INFO', res.data.userInfo)
            commit('SET_PERMISSIONS', res.data.permissions)
            resolve()
          })
          .catch(error => {
            reject(error)
          })
      })
    },

    // 用户信息同步
    userInfoAsync({ commit }, userInfo) {
      commit('SET_NAME', userInfo.username)
      commit('SET_AVATAR', userInfo.icon)
      commit('SET_ROLE', userInfo.note)
      commit('SET_CREATE_TIME', userInfo.createTime)
      commit('SET_PREV_LOGIN_TIME', userInfo.loginTime)
    },

    // 登出
    LogOut({ commit, state }) {
      return new Promise((resolve, reject) => {
        commit('SET_TOKEN', '')
        commit('SET_NAME', '')
        commit('SET_AVATAR', '')
        commit('SET_ROLE', '')
        commit('SET_CREATE_TIME', '')
        commit('SET_PREV_LOGIN_TIME', '')
        removeToken()
        resolve()
        router.push('/login')
      })
    },

    // 前端 登出
    FedLogOut({ commit }) {
      return new Promise(resolve => {
        commit('SET_TOKEN', '')
        removeToken()
        resolve()
      })
    }
  }
}

export default user

~~~

### 引入store

> 路径：src/store/index.js

~~~js
import Vue from 'vue'
import vuex from 'vuex'

// 引入子模块
import app from '@/store/modules/app'
import user from '@/store/modules/user'

Vue.use(vuex)

const store = new vuex.Store({
  modules: {
    app: app,
    user: user
  }
})

export default store

~~~



### 编写页面

> src/views/login/index.uve

~~~vue
<template>
  <div class="login_container">
    <div class="box">
      <!-- LOG区域 -->
      <div class="logo_name">
        ELITE
      </div>

      <!-- 标题区域 -->
      <div class="title_box">
        <h3>欢迎来到ELITE</h3>
        <p>登录后，查看更多</p>
      </div>

      <!-- 登录区域 -->
      <div class="login_box">
        <el-form
          :model="loginForm"
          :rules="loginFormRules"
          ref="loginFormRef"
          label-width="0px"
        >
          <!-- 用户名 -->
          <el-form-item prop="username">
            <el-input
              v-model="loginForm.username"
              prefix-icon="fas fa-user-astronaut"
              clearable
              @keyup.enter.native="login"
            >
            </el-input>
          </el-form-item>

          <!-- 密码 -->
          <el-form-item prop="password">
            <el-input
              v-model="loginForm.password"
              prefix-icon="fas fa-lock"
              type="password"
              show-password
              clearable
              @keyup.enter.native="login"
            >
            </el-input>
          </el-form-item>

          <!-- 按钮区域 -->
          <el-form-item>
            <el-button
              @click="login"
              type="success"
              v-loading.fullscreen.lock="fullscreenLoading"
              round
            >
              登录
            </el-button>
          </el-form-item>
          <!-- <p class="no_account_tips"><small>还没有账号?</small></p>
          <el-button round>注册</el-button> -->
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 登录表单的数据绑定对象
      loginForm: {
        username: '',
        password: ''
      },
      // 登录表单的验证规则对象
      loginFormRules: {
        // 验证用户名是否合法
        username: [
          { required: true, message: '请输入账号', trigger: 'blur' },
          { min: 4, max: 15, message: '长度在 4 到 15 个字符', trigger: 'blur' }
        ],
        // 验证密码是否合法
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      },
      // 控制loading组件
      fullscreenLoading: false
    }
  },
  methods: {
    // 登录方法
    login() {
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) {
          return this.$notify.warning({
            title: '请输入账号和密码！',
            message: '登录失败！'
          })
        }
        this.fullscreenLoading = true
        this.$store
          .dispatch('Login', this.loginForm)
          .then(() => {
            // 通过编程式导航跳转到后台主页，路由地址是'/'
            this.$router.push('/')
          })
          .catch(() => {
            this.fullscreenLoading = false
          })
      })
    }
  },
  watch: {
    $route(to, from) {
      // 以服务的方式调用的 Loading 需要异步关闭
      this.$nextTick(() => {
        this.fullscreenLoading = false
      })
    }
  }
}
</script>

<style lang="less" scoped>
.input {
  font-size: 0.9rem;
}

.el-form {
  position: absolute;
  bottom: 0;
  width: 70%;
  padding: 0 20px;
  box-sizing: border-box;
  margin: 0 auto;
  left: 50%;
  transform: translate(-50%, 0);
}

.no_account_tips {
  text-align: center;
}

.el-button {
  width: 100%;
}

.title_box {
  text-align: center;
  font-family: 'open sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 13px;
  p {
    font-size: 13px;
    color: #676a6c;
  }
}

h3 {
  font-weight: 600;
  font-size: 16px;
  color: #676a6c;
}

.box {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.logo_name {
  color: #e6e6e6;
  font-size: 180px;
  font-weight: 800;
  letter-spacing: -10px;
  text-align: center;
  font-family: none;
}

.login_box {
  width: 450px;
  height: 270px;
  border-radius: 3px;
}

.login_container {
  background-color: #f3f3f4;
  height: 100%;
}
</style>

~~~



很明显，看到右上角

![image-20200719112244774](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233132-861498.png)



### 完善退出

> 路径：src/views/layout/headBar.vue

~~~vue
<template>
  <div
    :style="{ background: themeColor }"
    :class="[collapse ? 'position-collapse-left' : 'position-left', 'headbar']"
  >
    <!-- 导航收缩 -->
    <span class="hamburg">
      <hamburger></hamburger>
    </span>

    <!-- 测试语言选择组件 -->
    <span style="color:#fff">
      <span>
        {{ $t('common.home') }}
      </span>
      <span>
        {{ $t('common.doc') }}
      </span>
      <span>
        {{ $t('common.blog') }}
      </span>
    </span>

    <!-- 工具栏 -->
    <span class="toolbar">
      <el-menu
        class="el-menu-demo"
        :background-color="themeColor"
        :active-text-color="themeColor"
        text-color="#14889A"
        mode="horizontal"
      >
        <!-- 主题切换 -->
        <el-menu-item index="1">
          <theme-picker class="theme-picker" :default="themeColor">
          </theme-picker>
        </el-menu-item>

        <!-- 语言切换 -->
        <el-menu-item index="2">
          <language-select></language-select>
        </el-menu-item>

        <!-- 用户信息 -->
        <el-menu-item index="3">
          <span class="user-info">
            <span>{{ user.name }}</span>
            <img :src="user.avatar" />
            <el-button @click="logout" icon="fa fa-sign-out" size="mini">{{
              $t('tips.exit')
            }}</el-button>
          </span>
        </el-menu-item>
        <!-- 头部右边区域 -->
        <!-- <span class="top-right">
      <el-button type="info">退出</el-button>
    </span> -->
      </el-menu>
    </span>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Hamburger from '@/components/Hamburger'
import ThemePicker from '@/components/ThemePicker'
import LanguageSelect from '@/components/LanguageSelect'
export default {
  components: {
    Hamburger,
    ThemePicker,
    LanguageSelect
  },
  data() {
    return {
      user: {
        name: 'Saul.J.Wu',
        avatar: 'https://s1.ax1x.com/2020/07/19/URgwyn.jpg',
        role: '超级管理员',
        registeInfo: '注册时间：2018-12-20 '
      }
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('LogOut')
      // 提示信息
      this.$notify.success({
        title: '退出成功！',
        message: ''
      })
    }
  },
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style lang="scss" scoped>
.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}

.headbar {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 1030;
  height: 60px;
  line-height: 60px;
  border-color: rgba(180, 190, 190, 0.8);
  border-left-width: 1px;
  border-left-style: solid;
}

.user-info {
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  img {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    margin-right: 10px;
  }
  span {
    margin-right: 10px;
  }
}

.navbar {
  float: left;
}
.hamburg,
.navbar {
  float: left;
}
.toolbar {
  float: right;
}
</style>

~~~



![image-20200719124042160](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233139-999521.png)



## 动态加载菜单

### 添加store

- 我们先添加几个store状态，后续需要用来共享使用。首先在store/modules下的app.js中添加一个menuRouteLoaded状态，判断路由是否加载过
- 然后在store/modules下新建一个menu.js，在index.js中引入，里面保存着加载后的导航菜单树数据。

`@/store/modules/menu.js`

~~~js
import { getMenuList } from '@/http/modules/menu'

const menu = {
  state: {
    // 导航菜单树
    menuList: [],
    // 菜单和路由是否已经加载
    menuRouteLoaded: false,
    // 默认激活的链接地址
    activePath: '',
    // 1级菜单名称
    menuNameLevel1: '',
    // 2级菜单名称
    menuNameLevel2: ''
  },
  getters: {
    // 对应着上面state
    menuList: state => state.menuList,
    menuRouteLoaded: state => state.menuRouteLoaded,
    activePath: state => state.activePath,
    menuNameLevel1: state => state.menuNameLevel1,
    menuNameLevel2: state => state.menuNameLevel2
  },
  mutations: {
    SET_MENU_LIST: (state, menuList) => {
      // 设置导航菜单树
      state.menuList = menuList
    },
    // 改变菜单和路由的加载状态
    SET_MENU_ROUTE_LOADED: (state, menuRouteLoaded) => {
      state.menuRouteLoaded = menuRouteLoaded
    },
    //清空面包屑
    RESET_MENU_LEVEL: state => {
      state.menuNameLevel1 = ''
      state.menuNameLevel2 = ''
    },
    //保存面包屑
    SET_MENU_LEVEL: (state, leve1, level2) => {
      state.menuNameLevel1 = leve1
      state.menuNameLevel2 = level2
    },
    SET_ACTIVE_PATH: (state, activePath) => {
      state.activePath = activePath
    }
  },
  actions: {
    /**
     * 获取菜单
     */
    GetMenu({ commit }) {
      return new Promise((resolve, reject) => {
        getMenuList()
          .then(res => {
            if (res.code === 403) {
              return reject(res)
            }
            if (res.code !== 200) {
              return reject(res)
            }
            console.log(res.data)
            commit('SET_MENU_LIST', res.data)
            commit('SET_MENU_ROUTE_LOADED', true)
            resolve()
          })
          .catch(error => {
            reject(error)
          })
      })
    },
    /**
     * 保存当前一级及二级菜单名称
     * @param {一级菜单名称} level1
     * @param {二级菜单名称} level2
     */
    SET_BREAD_TEXT({ commit }, level1, level2) {
      commit('SET_MENU_LEVEL', level1, level2)
    },
    /**
     * 清空面包屑
     */
    RESET_BREAD_TEXT({ commit }) {
      commit('RESET_MENU_LEVEL')
    },
    /**
     * 保存默认激活地址路径
     * @param {地址路径} activePath
     */
    activePathAsync({ commit }, activePath) {
      commit('SET_ACTIVE_PATH', activePath)
    }
  }
}

export default menu

~~~



- 在store/modules下新建一个permission.js，在index.js中引入，里面保存着用户的权限数据。

`@/store/modules/permissions.js`

~~~js
export default {
  state: {
    permissions: [] // 用户权限标识集合
  },
  getters: {

  },
  mutations: {
    SET_PERMISSIONS: (state, permissions) => { // 用户权限标识集合
      state.permissions = permissions
    }
  },
  actions: {
    permissionsAsync({ commit }, permissions) {
      commit('SET_PERMISSIONS', permissions)
    }
  }
}

~~~



### 导入store

`@/store/index.js`

~~~js
import Vue from 'vue'
import vuex from 'vuex'

// 引入子模块
import app from '@/store/modules/app'
import user from '@/store/modules/user'
import menu from '@/store/modules/menu'
import permission from '@/store/modules/permission'

Vue.use(vuex)

const store = new vuex.Store({
  modules: {
    app: app,
    user: user,
    menu: menu,
    permission: permission
  }
})

export default store

~~~



### 添加api

	`@/http/modules/menu.js`

~~~js
import axios from '@/http/axios'

/**
 * 菜单管理模块
 */

export const getMenuList = () => {
  return axios({
    url: '/menus',
    method: 'get'
  })
}

~~~

### 导入api

`@/http/api.js`

~~~js
// 接口统一集成模块
import * as login from '@/http/modules/login'
import * as user from '@/http/modules/user'
import * as menu from '@/http/modules/menu'

// 默认全部导出
export default {
  login,
  user,
  menu
}

~~~



### 新建菜单树组件

新建`@/components/MenuTree/index.vue`

~~~vue
<template>
  <div class="menuContainer">
    <!-- 侧边菜单区域 -->
    <el-menu
      :default-active="activePath"
      :collapse="collapse"
      background-color="#2F4050"
      active-text-color="#0dbc79"
      text-color="#fff"
      :unique-opened="true"
      :collapse-transition="false"
      :router="true"
    >
      <template v-for="item in menuList">
        <!-- 没子级菜单的一级菜单 -->
        <el-menu-item
          v-if="item.children.length == 0"
          :key="item.id"
          :index="'/'"
          @click="openMenu(item)"
        >
          <!-- 一级菜单的图标 -->
          <i :class="item.icon" style="margin-right:5px;"> </i>
          <!-- 一级菜单的文本 -->
          <span>{{ item.name }}</span>
        </el-menu-item>

        <!-- 有子级菜单的一级菜单 -->
        <el-submenu
          v-else
          :key="item.id"
          :index="item.id"
          @click.native="openMenu(item)"
        >
          <!-- 一级菜单的模板区域 -->
          <template slot="title">
            <!-- 一级菜单的图标 -->
            <i :class="item.icon"> </i>
            <!-- 一级菜单的文本 -->
            <span>{{ item.name }}</span>
          </template>
          <!-- 二级菜单 -->
          <el-menu-item
            @click="clickMenuLevel2(item, subItem)"
            :index="subItem.uri"
            v-for="subItem in item.children"
            :key="subItem.id"
          >
            <template slot="title">
              <!-- 二级菜单的图标 -->
              <i
                :class="subItem.icon !== null ? subItem.icon : 'el-icon-menu'"
              ></i>
              <!-- 二级菜单的文本 -->
              <span>{{ subItem.name }}</span>
            </template>
          </el-menu-item>
        </el-submenu>
      </template>
    </el-menu>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'menu-tree',
  methods: {
    // 打开一级菜单
    openMenu(obj) {
      if (obj.name === '首页') {
        this.$store.dispatch('activePathAsync', '')
        // 清空面包屑导航
        this.$store.dispatch('RESET_BREAD_TEXT')
        this.$router.push('/')
      }
    },
    // 点击二级菜单按钮保存面包屑
    clickMenuLevel2(father, children) {
      this.$store.dispatch('SET_BREAD_TEXT', father.name, children.name)
    }
  },
  components: {},
  computed: {
    ...mapState({
      menuList: state => state.menu.menuList,
      activePath: state => state.menu.activePath,
      collapse: state => state.app.collapse
    })
  }
}
</script>

<style lang="scss" scoped>
.menuContainer {
  .el-menu {
    height: 100%;
    text-align: left;
  }
  i {
    margin-right: 5px;
    font-size: 16px;
    text-align: left;
  }
}

.el-menu--collapse {
  .el-submenu__title {
    span {
      display: none;
    }
  }
  .el-menu-item {
    span {
      display: none;
    }
  }
}
</style>

~~~



### 导入菜单组件

在navBar.vue中引入

~~~vue
<template>
  <div
    :class="[
      collapse ? 'menu-bar-collapse-width' : 'menu-bar-width',
      'menu-bar-container'
    ]"
  >
    <!-- logo -->
    <div
      @click="$router.push('/')"
      class="logo"
      :style="{ background: themeColor }"
      :class="collapse ? 'menu-bar-collapse-width' : 'menu-bar-width'"
    >
      <img src="@/assets/logo.png" />
      <div>{{ collapse ? '' : appName }}</div>
    </div>

    <!-- 导航菜单 -->
    <div style="height:100%">
      <menu-tree style="height:100%"></menu-tree>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import MenuTree from '@/components/MenuTree'
export default {
  data() {
    return {}
  },
  methods: {},
  components: {
    MenuTree
  },
  computed: {
    ...mapState({
      themeColor: state => state.app.themeColor,
      collapse: state => state.app.collapse,
      appName: state => state.app.appName
    })
  }
}
</script>

<style lang="scss" scoped>
.el-menu {
  position: absolute;
  top: 60px;
  bottom: 0px;
  text-align: left;
  // background-color: #2968a30c;
}

.menu-bar-container {
  position: fixed;
  top: 0px;
  left: 0;
  bottom: 0;
  z-index: 1020;
  .logo {
    height: 60px;
    line-height: 60px;
    background: #545c64;
    cursor: pointer;
    img {
      width: 40px;
      height: 40px;
      border-radius: 0px;
      margin: 10px 10px 10px 10px;
      float: left;
    }
    div {
      font-size: 25px;
      color: white;
      text-align: left;
      padding-left: 20px;
    }
  }
}
.menu-bar-width {
  width: 200px;
}
.menu-bar-collapse-width {
  width: 65px;
}
</style>

~~~





### 导航守卫

未登录不能查看详细信息

> 路径：src/router/index.js

~~~js
import Vue from 'vue'
import VueRouter from 'vue-router'
import { getToken } from '@/utils/auth'
import store from '@/store'

Vue.use(VueRouter)

const router = new VueRouter({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: () => import('@/views/home/index')
    },
    {
      path: '/login',
      name: 'Login',
      component: () => import('@/views/login/index')
    }
  ]
})

/**
 * 导航守卫
 * to 将要访问的路径
 * from 代表从哪个路径来
 * next 是一个函数，表示放行，有2种方式
 * 其中next() 放行 ，next('/login') 强制跳转
 */
router.beforeEach((to, from, next) => {
  // 如果访问的是 登录页面或者注册页面，直接放行（注册页面后期写）
  if (to.path === '/login') {
    return next()
  }
  const token = getToken()

  // 如果token为空，直接强制跳转到登录页面
  if (!token) {
    return next('/login')
  }
  // 如果token不为空,判断是否已经加载了菜单和权限
  if (!store.state.menu.menuRouteLoaded) {
    // 没加载，则加载菜单和权限
    console.log('动态菜单和路由不存在，开始加载菜单和权限...')
    store.dispatch('GetMenu')
  }
  // 最后直接放行
  next()
})

export default router

~~~





## 添加面包屑组件

### 核心代码：

![image-20200726193047206](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233709-662935.png)

![image-20200726193052163](https://raw.githubusercontent.com/SaulJWu/typora-plugins-win-img/master/typora/202008/13/233712-412083.png)

### 完整代码

`mainContent.vue`

~~~vue
<template>
  <div
    class="main-container"
    :class="collapse ? 'position-collapse-left' : 'position-left'"
  >
    <!-- 面包屑导航 -->
    <div class="mgb15">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <!-- 0级面包屑 -->
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <!-- 1级面包屑 -->
        <el-breadcrumb-item v-if="menuNameLevel1">{{
          menuNameLevel1
        }}</el-breadcrumb-item>
        <!-- 2级面包屑 -->
        <el-breadcrumb-item v-if="menuNameLevel2">{{
          menuNameLevel2
        }}</el-breadcrumb-item>
      </el-breadcrumb>
    </div>

    <!-- 卡片视图区域 -->
    <el-card>
      <!-- 主内容区域 -->
      <div class="main-content">
        <keep-alive>
          <transition name="fade" mode="out-in">
            <router-view></router-view>
          </transition>
        </keep-alive>
      </div>
    </el-card>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {}
  },
  methods: {},
  components: {},
  computed: {
    ...mapState({
      collapse: state => state.app.collapse,
      menuNameLevel1: state => state.menu.menuNameLevel1,
      menuNameLevel2: state => state.menu.menuNameLevel2
    })
  }
}
</script>

<style lang="scss" scoped>
.mgb15 {
  margin: 15px;
}

.bread-text {
  font-size: 16px;
}

.el-card {
  min-height: 1000px;
}

.main-container {
  padding: 0 5px 5px;
  position: absolute;
  top: 80px;
  right: 1px;
  bottom: 0px;
  background: rgba(67, 69, 70, 0.1);
  .main-content {
    position: absolute;
    top: 45px;
    left: 5px;
    right: 5px;
    bottom: 5px;
    padding: 5px;
  }
}
.position-left {
  left: 200px;
}
.position-collapse-left {
  left: 65px;
}
</style>

~~~



## vue单页面应用刷新网页后vuex的state数据丢失的解决方案

直接放再app.vue

~~~js
export default {
  name: 'App',
  created () {
    //在页面加载时读取sessionStorage里的状态信息
    if (sessionStorage.getItem("store") ) {
        this.$store.replaceState(Object.assign({}, this.$store.state,JSON.parse(sessionStorage.getItem("store"))))
    } 

    //在页面刷新时将vuex里的信息保存到sessionStorage里
    window.addEventListener("beforeunload",()=>{
        sessionStorage.setItem("store",JSON.stringify(this.$store.state))
    })
  }
}
~~~