title: React类组件
tags: []
top_img: >-
  https://img2.baidu.com/it/u=2072364302,1284571828&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500
cover: >-
  https://img2.baidu.com/it/u=2072364302,1284571828&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500
categories: []
date: 2023-04-12 20:16:00
---

#  React 类组件

##  1. 组件概述

目标：了解组件的作用和 React 组件的创建方式

什么是组件

组件设计思想

###   1-1. 什么是组件

我们可以将组件理解为可以被组合的零部件。

{% asset_img 1.png This is an example image %}

React 采用组件化的方式构建用户界面。

先将一个完整的页面拆分为许许多多的小零件，再将这些小零件组合起来形成一个完整的页面

{% asset_img 2.png This is an example image %}

组件就是用户界面当中的一块独立的区域，在组件内部会包含这块区域中的视图代码、样式代码以及逻辑代码。

{% asset_img 3.png This is an example image %}

###  1-2. 组件设计思想

目标：掌握组件化开发方式为开发者带来的好处

组件的核心思想之一就是复用，定义一次到处使用。

组件可以用来封装用户界面中的重复区块，复用重复区块

{% asset_img 4.png This is an example image %}

##  2. 创建组件

目标：掌握创建类组件的方式

```react
// src/index.js
import ReactDOM from "react-dom/client";
import React from "react";

// 1. 组件名称首字母大写, 因为组件是通过标签的方式调用的, React 通过标签的首字母判定它是组件还是普通标记
// 2. 只有继承了 Component 类才是 React 组件
// 3. 类中必须包含 render 方法用于渲染用户界面, render 方法的名字是固定的, 渲染用户界面时返回 jsx, 不渲染任何界面时返回 null,
class App extends React.Component {
  render() {
    return <div>头部组件</div>;
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

在实际的 React 项目开发中，组件作为独立的个体一般都会被放置在单独的文件中方便维护。

```react
// src/App.js
import React from "react";

// 约定: 组件文件的名称和组件名称保持一致
class App extends React.Component {
  render() {
    return <div>应用的根组件</div>;
  }
}
// 导出组件, 以便在其他地方导入并使用组件
export default App;
```

```react
// src/index.js
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

##   3. 组件级样式

目标：掌握为 React 组件添加组件级样式的方式。

组件级样式是指样式只在当前组件中生效，当前组件中应用的样式不会溢出到组件外部从而影响页面中的其他部分。

```css
/* src/App.module.css */
.page {
  width: 100%;
}

.page .header {
  height: 85px;
}

.page .header .logo {
  width: 100px;
  height: 100%;
}
```

```react
// src/App.js
import React from "react";
import styles from "./App.module.css";

export default class App extends React.Component {
  render() {
    return (
      <div className={styles.page}>
        <div className={styles.header}>
          <div className={styles.logo}></div>
        </div>
      </div>
    );
  }
}
```

React 中组件级样式的实现依赖于 webpack 提供的 CSS 模块功能。

在构建应用的过程中，webpack 会为当前组件使用的类名进行重命名。

在重新命名的类名中使用 [组件名称 + 原始类名 + 随机字符串]，从而保证类名下的样式不会溢出到组件外部。

{% asset_img 5.png This is an example image %}

##  4. 组件状态概述

目标：掌握什么是组件状态

组件是用来构建用户界面的，组件状态表示的就是用户界面的状态。

用户界面状态是指在不同时刻或不同条件下为用户展示的不同的用户界面。

比如有一块将要展示用户列表的区域，用户列表数据需要从服务端获取。该区域将会有以下几种状态。

{% asset_img 6.png This is an example image %}

| 状态     | 解释                                             |
| -------- | ------------------------------------------------ |
| 空闲     | 在没有发出请求时该区域为空闲状态                 |
| 加载中   | 请求在发出后没有得到响应前该区域为加载中状态     |
| 加载成功 | 当请求得到响应用户列表渲染成功后该区域为成功状态 |
| 加载失败 | 当请求未得到正确的响应时该区域为失败状态         |
| 结束     | 不论请求成功与失败请求都结束了该区域为结束状态   |

再比如导航链接，它具有默认状态和选中状态。下拉框，它具有收缩状态和展开状态。

{% asset_img 7.png This is an example image %}

那么如何在程序中表示用户界面(UI)的状态呢？在程序中可以通过声明变量进行状态的记录。

```javascript
// idle: 空闲状态
// loading: 加载中
// success: 加载成功
// error: 加载失败
// finish: 结束
let status = "idle";
```

```react
let navLink = "白色";
let activeNavLink = "绿色"
```

##  5. 声明组件状态

总体目标：实现计数器案例，即声明组件状态 count 用于存储数值，点击按钮让数值 + 1。

在类组件中，组件状态被存储在一个名字为 state 的类属性中，该属性值的类型是对象，对象中的属性即为组件状态。

```react
class App extends React.Component {
  state = {
    count: 0,
  };
}
```

##  6. 获取组件状态

```react
class App extends Component {
  render() {
    // render 方法中的 this 指向组件的实例对象
    // state 属性是类的实例属性
    // 所以通过 this 是可以获取到 state 对象的
    return <button>{this.state.count}</button>;
  }
}
```

##  7. 修改组件状态

类组件中的组件状态必须通过类实例对象下的 setState 方法进行修改，setState 方法接收新状态作为参数。

当前组件实例下并没有 setState 方法，setState 方法是父类 Component 提供的。

组件状态发生变化会触发视图自动更新，所以在页面中点击按钮时我们可以实时看到状态的变化。

```react
class App extends Component {
  render() {
    return (
      <button onClick={() => this.setState({ count: this.state.count + 1 })}></button>
    );
  }
}
```

##  8. 状态不可变理念

目标：理解 React 中状态不可变理念

在 React 中关于状态有一核心理念，就是状态不可变，该理念需要被严格遵守。

状态不可变是指在更新组件状态时不能直接操作现有状态，而是要基于现有状态值产生新的状态值。

```react
state = {
  count: 0,
  list: [1, 2, 3],
  person: {
    name: "张三",
    age: 18,
  },
};
```

```react
// 错误写法
this.state.count = 100;
this.state.count++; // this.state.count = this.state.count + 1
this.state.list.push(4); // push pop shift unshift splice sort reverse
this.state.person.name = "李四";
```

```react
// 正确写法
this.setState({
  count: this.state.count + 1,
  list: [...this.state.list, 4],
  person: {
    ...this.state.person,
    age: 30,
  },
});
```

```react
this.setState({
  // 数组的删除写法
  list: [...this.state.list.slice(0, 1), ...this.state.list.slice(2)],
});

this.setState({
  // 数组的修改写法
  list: [...this.state.list.slice(0, 1), 4, ...this.state.list.slice(2)],
});
```

如何理解 React 状态不可变？

因为 React 在更新真实 DOM 对象之前，要对新旧状态对象 state 进行对比找出要更新的部分，所以当前状态也就是旧状态是不能被直接更改的。

##  9. 状态调试工具

目标：安装 React 调试工具、掌握使用调试工具查看组件状态的方式

[React Developer Tools Chrom 插件离线安装包下载](https://chrome.zzzmh.cn/info/fmkadmapgofadopljbjfkapdkoienihi)

{% asset_img 8.png This is an example image %}

##  10. 复习 this 关键字 

目标：掌握 JavaScript 中 this 关键字的使用方式

this 翻译过来表示这个，它是一个代词，在不同的场景中 this 可以指代不同的事物。

在 JavaScript 代码运行的过程中，运行环境不同 this 也可以指代不同的对象，这个环境是指全局作用域、函数对应的局部作用域。

函数内部的 this 指向谁要看该函数是被谁调用起来的。

```javascript
console.log(this === window); // true
```

```javascript
function fn () {
  console.log(this);
}
fn();

// --------------------------

// 在全局作用域下通过 function 关键字声明的函数会被自动挂载到 window 对象上
console.log(window.fn)
// 所以在调用 fn 函数时可以写成下面这种形式
window.fn()
// 由于函数是被 window 调用起来的, 所以函数内部的 this 关键字指向了 window
// 又由于在访问全局作用域下的属性和方法时可以省略全局对象, 所以最终代码写成了以下形式
fn();
```

```javascript
function showName() {
  console.log(this.name);
}

var student = {
  name: "张三",
  showName,
  other: {
    name: "李四",
    showName,
  },
};
student.showName(); // 张三
student.other.showName(); // 李四
```

```javascript
var name = "王五";
var student = {
  name: "张三",
  showName() {
    console.log(this.name);
  },
};

student.showName(); // 张三
var showName = student.showName;
showName(); // 王五
```

```javascript
// 箭头函数内部不绑定 this
// 在箭头函数中使用的 this 实际上是箭头函数本身定义处作用域的 this
var student = {
  name: "张三",
  showName() {
    var test = () => {
      console.log(this);
    };
    test();
  },
};
student.showName();
const showName = student.showName;
showName();
```

##  11. 类组件方法中的 this

目标：掌握类组件中事件处理函数 this 关键字的指向如何更改

1. 了解类组件中默认提供的方法中 this 指向谁

2. 了解类组件中事件处理函数中的 this 指向谁

3. 掌握将类组件中更改事件处理函数中 this 指向的方式

① 在类组件中 render 方法、constructor 方法中的 this 关键字指向当前类的实例对象。

```react
export default class App extends React.Component {
  constructor() {
    super();
    console.log("constructor", this);
  }
  render() {
    console.log("render", this);
    return null;
  }
}
```

② 类组件中元素事件的事件处理函数中的 this 指向 undefined

```react
export default class App extends React.Component {
  clickHandler() {
    console.log(this);
  }
  render() {
    return <div onClick={this.clickHandler}>Hello React</div>;
  }
}
```

而在大多数情况下，我们都希望事件处理函数中的 this 关键字指向组件实例对象，因为只有这样我们在更改组件状态时才能调用到 setState 方法。

③ 将类组件中事件处理函数中的 this 更改为组件实例的几种方式 

```react
class App extends Component {
  onClickHandler() {
    console.log(this);
  }
  render() {
    return <button onClick={() => this.onClickHandler()}>button</button>;
  }
}
```

```react
class App extends Component {
  // 将事件处理函数改写成箭头函数
  // 问题: 事件处理函数从原型方法变成了实例方法, 如果当前组件会被调用很多次, 就会产生很多个相同的事件处理函数, 浪费内存空间.
  onClickHandler = () => {
    console.log(this);
  };
  render() {
    return <button onClick={this.onClickHandler}>button</button>;
  }
}

// 为什么改写成箭头函数以后可以解决 this 问题?
// 简写语法
class Person {
  fn = () => {}
}

class Person {
  constructor () {
    // 由于箭头函数不绑定 this, 所以 fn 函数在被调用后, 函数内部的 this 实际上用的是 constructor 构建函数中的 this
    // 而构造函数中的 this 指向了组件实例对象, 所以 fn 函数中的 this 就指向了实例对象
    this.fn = () => {}
  }
}
```

```react
class App extends Component {
  onClickHandler() {
    console.log(this);
  }
  render() {
    // 通过 bind 方法将事件处理函数中的 this 指向组件实例对象, bind 方法返回一个新的被更改了 this 指向的函数作为事件处理函数
    // 问题: render 方法每次重新执行都会为元素绑定新的有bind 方法返回的事件处理函数, 性能有一丢丢损失
    return <button onClick={this.onClickHandler.bind(this)}>button</button>;
  }
}
```
```react
class App extends Component {
  constructor() {
    super();
    // 在构造函数中将事件处理函数更改为组件对象
    // 构造函数中的 this 指向的是组件的实例对象
    // 这样即保证了事件处理函数为原型方法, 又确保了 this 指向的更改只执行一次
    // 所以从性能角度考虑, 这种方式是最为理想的
    // 推荐: ⭐️⭐️⭐️⭐️⭐️
    this.onClickHandler = this.onClickHandler.bind(this);
  }
  onClickHandler() {
    console.log(this);
  }
  render() {
    return <button onClick={this.onClickHandler}>button</button>;
  }
}
```
##  12. 非受控表单

目标：掌握非受控表单的使用方式

非受控表单是指用户在表单中输入的内容由表单自身进行管理。

开发者若要获取表单控件中的值需要手动获取表单元素，再通过 DOM 的方式获取表单值。

所以当前我们主要学习如何通过 React 提供的方式获取 DOM 对象。

```react
import { Component, createRef } from "react";

class App extends Component {
  constructor() {
    super();
    // 设置事件处理函数中的 this 关键字指向组件实例对象
    this.onClickHandler = this.onClickHandler.bind(this);
  }
  // createRef: 创建元素的引用对象
  inputRef = createRef();
  // 按钮点击事件的事件处理函数
  onClickHandler() {
    // 通过文本框的元素引用对象获取文本框状态
    console.log(this.inputRef.current.value);
  }
  render() {
    return (
      <>
      	{/* 为元素引用对象绑定元素 */}
        <input type="text" ref={this.inputRef} />
				{/* 点击按钮时获取文本框控件自身管理的状态 */}
        <button onClick={this.onClickHandler}>button</button>
      </>
    );
  }
}
```

##  13. 受控表单

目标：掌握受控表单的使用方式、理解受控组件的执行过程

1. 什么是受控表单
2. 如何实现受控表单
3. 受控表单的代码执行顺序分析

① 什么是受控表单

受控表单是指用户在表单中输入的内容由组件状态进行管理。

就是说用户在表单中输入内容时，该内容会被实时同步给组件状态，开发者要想获取用户在表单中输入的内容只需要获取组件状态即可。

② 受控表单的实现方式

使用表单控件的 value 属性将组件状态与表单控件进行绑定。

使用表单控件的 onChange 事件实现表单控件值和组件状态进行同步。

```react
class App extends Component {
  state = {
    text: "默认值",
  };
  onChangeHandler = (event) => {
    // 调用 setState 方法更新组件状态
    // 将组件状态的值更新为用户在文本框中输入的内容
    this.setState({
      text: event.target.value,
    });
  }
  render() {
    return (
      <input
        type="text"
        {/* 将组件状态和文本框的 value 属性进行绑定 */}
        value={this.state.text}
        {/* 为文本框绑定 change 事件, 当用户在文本框中输入时更新组件状态 */}
        onChange={this.onChangeHandler}
      />
    );
  }
}
```
说白了 React 中的受控表单其实就是 Vue 中的双向数据绑定。

注意：在只为表单控件添加 value 属性而没添加 onChange 事件的情况下，浏览器控制台会报警告。

```react
<input type="text" value={this.state.text} />
```
你为表单控件供了 value 属性但是没有提供 onChange 事件，这将渲染一个只读的表单控件(用户无法在表单控件中输入内容)。

如果你只是想为文本框设置一个默认值，你应该使用 defaultValue。

如果你想实现受控表单请添加 onChange 事件将表单内容同步给组件状态。

如果只为表单控件绑定 value 属性后产生的行为符合你的预期，为表单控件添加 readOnly 属性以消除警告。

总结：在受控表单中，表单控件身上必须同时具有 value 属性和 onChange 事件。

③ 受控表单执行过程

(1) 用户触发表单控件的 onChange 事件，执行 onChange 事件的事件处理函数

(2) 在事件处理函数中通过事件对象获取到表单控件的最新状态并使用最新状态更新组件状态

(3) 组件状态更新完成后 render 方法重新执行，在 render 方法中通过最新的组件状态渲染视图











