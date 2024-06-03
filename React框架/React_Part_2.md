# React Part 2

## Table of Contents

- [前端工程化与 React](#前端工程化与-react)
- [React 的特性](#react-的特性)
  - [命令式 VS 声明式](#命令式-vs-声明式)
  - [组件化](#组件化)
- [创建 React App](创建-react-app)
- [React 是简单易用的框架](#react-是简单易用的框架)
- [如何搭建 React 项目](#如何搭建-react-项目)

## 前端工程化与 React

- JavaScript(Vanilla JS | Node.js)

  - Vanilla JavaScript 是指原生 JavaScript，未经任何库或者框架修改的纯粹的 JavaScript。它不依赖于任何外部库，如 jQuery 或 React。
  - 使用 Vanilla JavaScript 操作前端页面，引入了 DOM.

- DOM（Document Object Model，文档对象模型）: 是一个编程接口，它允许 JavaScript 动态地访问和更新文档内容、结构和样式。当浏览器加载页面时，他会创建页面的文档对象模型。DOM API 就是让开发者可以通过变成方式与 DOM 交互的一组方法和属性。

  > 参考 MDN: [Document Object Model (DOM)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

  - DOM API 是框架和库操作浏览器的唯一方法
  - 由于 Vanilla JavaScript 自身存在的问题（语法复杂、可读性差等），jQurey 被引入。

- JQuery

  - 跨浏览器的兼容性
  - 简化的语法
  - 易用的 AJAX 语法
  - 强大的选择器引擎

  > 虽然 jQurey 极大地简化了前端开发，但其在处理大型、复杂应用时的局限性导致了现代框架和库的出现。

## React 的特性

- Declarative 声明式编程
- Component-Based 组件化

### 命令式 VS 声明式

命令式编程和声明式编程是两种不同的编程范式，它们在解决问题和描述程序行为的方式上有所不同。

1. 命令式：（注重**过程**而不是结果）

   - 命令式编程强调编写详细的指令，告诉计算机如何执行任务。
   - 开发者需要显式地指定每个步骤和每个操作的执行顺序。
   - 代码通常包含大量的控制结构（如循环和条件语句）和副作用（直接修改状态）。

   ```js
   const db = sql.connect(str);
   const table = db.readTable("student");
   const result = [];

   for (let i = 0; i < table.data.length; i++) {
     if (table.data[i].score < 50) {
       result.push(table.data[i]);
     }
   }

   result.slice(0, 10);
   ```

2. 声明式：（注重**结果**而不是过程）

   - 声明式编程更关注描述问题的解决方案，而不是具体的实现细节。
   - 开发者描述所需的结果，而不是详细说明如何达到这个结果。
   - 代码更加简洁、易读和易维护，因为它们通常更抽象，不涉及具体的操作步骤。

   ```sql
   SELECT name, score, id FROM student WHERE score < 50
   ```

> 💡 总的来说，随着前端应用的复杂性不断增加，从命令式到声明式的转变已经成为了一种必然。这种转变为前端开发带来了更高的效率，可读性和可维护性，从而支持了大规模项目的持续发展和创新。

**Example**

```js
<button id="alertButton">Show Alert</button>

<script>
  document.getElementById('alertButton').addEventListener('click', function()) {
    alert('Button was clicked!');
  }
</script>
```

```js
import React from "react";

function AlertButton() {
  return (
    <button onClick={() => alert("Button was clicked!")}>Show Alert</button>
  );
}

export default AlertButton;
```

上面的两个例子都达到了同样的效果，但是方法不同：

- Vanilla JS，使用了命令式，明确描述了如何操作 DOM
- React，使用了声明式，只描述了界面应该如何呈现。实际的 DOM 操作是 react 库在背后处理的。

### 组件化

组件化是为解决以下前端项目问题而产生的：

- 复杂性增加
- 代码重复与冗余
- 难以维护
- 团队协作困难
- 缺乏 UI 和功能的一致性

而组件化就像乐高积木一样：

- 模块化与可重用性
- 简单与清晰的结构
- 易于维护
- 团队协作

## 创建 React App

- [React](https://react.dev/): 一个专注于 UI 的 JavaScript 库
- [Babel](https://babeljs.io/): 让现代 JavaScript 兼容所有浏览器，引入非标准化的 JavaScript 版本。
- [Webpack](https://webpack.js.org/): 模块捆绑器和任务运行器

## React 是简单易用的框架

- JS 是命令式的，React 是声明式的
- 不要神话 React！React 是简单的，可读的，组件化的
- 在 IT 中一定是简单易用的技术才能存活下来
- 不要想复杂的东西

## 如何搭建 React 项目

### 使用脚手架搭建

- 脚手架是一个工具，帮我们创建项目的基本功能，包括 Babel 的配置
  - vite 脚手架 `npm create vite my-project-name -- --template react`
    - 为什么使用 vite， vite 比 create react app 好在哪？
      - 因为简单 上手快 好学
      - Junior 不要谈 performance
    - [vite 的官方文档](https://vitejs.dev/)

### 什么是打包器？

- webpack 是现在主流前端打包工具，但过于繁杂
- Rollup 正逐渐代替 webpack
- Turbo

### React App 基本架构

- `index.html` 是入口文件，所以要看一个 Web App 是怎么工作的，首先去看 `index.html`
- 根节点 `root` 和 树状结构 `tree`
  - 在 React 中，根节点通常是应用的顶层组件，它是整个组件树的起点。在 React 的`虚拟DOM`中，根节点是`真实DOM树`的入口点。通过`ReactDOM库`中的`ReactDOM.render()方法`，你可以将`React元素`渲染到一个`真实的DOM节点`上，这个节点就是根节点。
  - 组件树是由多个组件嵌套而成的层级结构，它描述了整个应用的组织和关系。组件树的结构反映了应用的 UI 结构，每个节点都代表一个 React 组件。
  - 什么是 `ReactDom.createRoot()`?
    - `ReactDom.createRoot`在`index.html`上创建了一个根节点
  - 什么是 `react.render()`?
    - `react.render()`在根节点上渲染了`<APP />`
  - 什么是 `ReactDom`?
    - `ReactDom`是一个桥梁，用于连接 React 和 HTML
- `React.StrictMode`
