---
title: React状态管理-hox
date: 2021-01-26 10:45:02
permalink: /pages/3fd726/
categories:
  - 前端
  - React
tags:
  - 
---
## 前言

作为一个刚接触react的人，我也就半学半做的学习react，react它只是帮我做了UI渲染，但是还需要一个状态管理。

这两天我一直在看B站，知乎，掘进,CSDN，发现拥抱hooks的人不多，像redux、mbox很多都使用class来写的，如果我的项目中，全是hook，用redux和mbox就很难受了。

再加上我比较菜，还没掌握redux和mbox，但是我又急需一个全局状态管理的数据流解决方案。

最终我找到了[hox](https://github.com/umijs/hox/blob/master/README-cn.md)。



## 安装

~~~bash
yarn add hox
~~~



## 快速上手

### 创建一个 model

在 hox 中，任意的 custom Hook，经过 `createModel` 包装后，就变成了持久化，且全局共享的数据。

```jsx
import { useState } from "react";
import { createModel } from "hox";

function useCounter() {
  const [count, setCount] = useState(0);
  const decrement = () => setCount(count - 1);
  const increment = () => setCount(count + 1);
  return {
    count,
    decrement,
    increment
  };
}

export default createModel(useCounter);
```

> 通过 `createModel` ， hox 会返回一个新的 custom Hook，用来获取 model 的数据。`createModel` 还可以接收第二个参数，便于[给 custom hook 传参](https://github.com/umijs/hox/blob/master/README-cn.md#给-custom-hook-传参)

### 使用 model

还记得刚刚 `createModel` 的返回值吗？在组件中调用这个 Hook ，就可以获取到 model 的数据了。

```jsx
import useCounterModel from "../models/counter";

function App(props) {
  const counter = useCounterModel();
  return (
    <div>
      <p>{counter.count}</p>
      <button onClick={counter.increment}>Increment</button>
    </div>
  );
}
```

`useCounterModel` 是一个真正的 Hook，会订阅数据的更新。也就是说，当点击 "Increment" 按钮时，会触发 counter model 的更新，并且最终通知所有使用 `useCounterModel` 的组件或 Hook。



实现了官方的demo之后就可以开始愉快的进行业务开发了。



## 进阶用法

### 给 custom hook 传参

当一个 custom hook 被用于不同的场景下，我们希望它们可以拥有不同的参数。

如下方的例子一样，我们可以通过 `createModel` 的第二个参数，为 custom hook 设置一个参数。这是设置初始值的最佳时机。

```jsx
import { useState } from "react";
import { createModel } from "hox";

function useCounter(initialValue) {
  const [count, setCount] = useState(initialValue ?? 0);
  const decrement = () => setCount(count - 1);
  const increment = () => setCount(count + 1);
  return {
    count,
    decrement,
    increment
  };
}

const useCounterModel = createModel(useCounter);
const useCounterModelWithInitialValue = createModel(useCounter, 20);
```

### model 之间的依赖

虽然你仍然可以按照传统的单一数据源的思想进行 model 的设计，但我们更推荐将 model 拆分成多个小部分，于是不可避免的，我们需要在多个 model 之间处理依赖关系，例如订单模块 `order` 依赖账户模块 `account` 。

在 hox 中，处理模块之间的依赖非常简单且自然：在一个 model 中可以直接使用 `useXXXModel` 来获取另一个 model，并订阅其更新，和在组件中使用并无两样。

> 提醒：小心循环依赖！

```jsx
import { useCounterModel } from "./counter";

export function useCounterDouble() {
  const counter = useCounterModel();
  return {
    ...counter,
    count: counter.count * 2
  };
}
```

### 只读不订阅更新

在某些场景下，我们只希望读取当前 model 的值，而不希望订阅其更新。

如下面的例子一样，我们可以通过 `useCounterModel.data` 来读取当前 model 中值，而不订阅它的更新。

> `useCounterModel.data` 不是一个 Hook，你可以在任何场景中使用它。

```jsx
import { useState } from "react";
import { useCounterModel } from "./counter";

export function logger() {
  const [log, setLog] = useState([]);
  const logCount = () => {
    const counter = useCounterModel.data;
    setLog(log.concat(counter));
  };

  return {
    log,
    logCount
  };
}
```

### 在类组件中使用

虽然 model 是使用的 Hooks 语法，但你仍然可以在类组件中获取和订阅 model ：

```jsx
class App extends Component {
  render() {
    const { counter } = this.props;

    return (
      <div>
        <p>{counter.count}</p>
        <button onClick={counter.increment}>Increment</button>
      </div>
    );
  }
}

export default withModel(useCounterModel, counter => ({
  counter
}))(App);
```





## 后话

虽然有很多大佬已经有现成的框架让我们去用

比如：

antdFront/README-cn.md at master · X-neuron/antdFront
https://github.com/X-neuron/antdFront/blob/master/README-cn.md



但是如果自己不实现一遍，感觉还是虚的很。

脚踏实地，等我掌握了，再来用他们的也不迟。先吃饱了再说。