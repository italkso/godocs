## 1.React

### React 简介

用于构建用户界面的JavaScript库 React，是React Native的核心。React 具有**声明式**、**异步**、**响应式**的特性。

声明式编程范式：描述程序应该达成什么目的。

异步：让代码语句从主程序流程中脱离，主程序代码在异步调用之后立即继续执行，而无需等待异步代码完成。

DOM没有对动态创建UI进行优化。

React 采用 虚拟DOM，利用观察者模型进行变动检测，通过差分算法（diffing algorithm，http://calendar.perfplanet.com/2013/diff/）判断最少的DOM操作。



开发简单，声明式编程，组件化开发

### React的工作原理

- **组件驱动开发**

  将UI拆解成组件，遵循**单一职责原则**（the single responsibility principle），即一个组件理论上只应该做一件事。

  每个组件拥有内部状态、逻辑、事件处理器（如点击按钮和改变表单输入）以及行内样式等。

- **交互式UI**

  通过**状态（state）**触发UI背后的数据模型的改变，一旦状态发生了改变，React 就重新渲染视图。

  **属性**（props）和**状态**（state）是 React 的两种数据模型，属性可以理解为组件的静态数据，而状态是动态的，两者都可以触发重新渲染。如果组件有时候需要修改自身的某个特性，就把这个特性归类于组件状态的一部分，除此以外便是组件的属性。



## 2. React Native 的工作原理

React Native应用借助宿主平台上的UI库，渲染真正的原生UI组件，不仅限于WebView。

React Native允许开发者通过JavaScript函数的代理，直接调用原生模块。

