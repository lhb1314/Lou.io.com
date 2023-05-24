---
title: React函数组件
date: 2023-04-13 14:59:39
tags:
top_img: https://www.linuxprobe.com/wp-content/uploads/2016/10/0-react01-1.jpg
cover: https://www.linuxprobe.com/wp-content/uploads/2016/10/0-react01-1.jpg
---

# React 函数组件

##  1. 创建组件
**目标：掌握在 React 中创建函数式组件的方式**

目前 React 官方更加推荐开发者使用函数的方式创建组件，在 React 新的[官方文档](https://beta.reactjs.org/)中所有示例代码也都要更新成了函数的方式。

函数组件其实就是一个返回视图 JSX 的函数

```react
// src/App.js
import React from "react"

function App() {
	return <div>App Works</div>
}

export default App;
```
```react
// src/index.js
import App from "./App";

root.render(<App />)
```

##  2. 声明组件状态 useState

**目标：掌握在函数组件中使用 useState 方法创建组件状态的方式**

① 在函数组件中开发者可以通过 useState 方法创建组件状态

```react
import React, {useState} from "react"

function App() {
	// useState 方法的第一个参数是状态的初始值
	// useState 方法的返回值是一个数组，数组中的第一个值是状态变量，数组中的第二个值为修改状态的方法
	// 开发者可以通过数组解构的方式获取状态变量和修改状态变量的方法
	// 修改状态变量的方法接收一个参数, 即新的状态值
    const [value, setValue] = useState("initialState");
    return (
    	<>
    		{/*
    			先渲染状态初始值 initialState
    			当按钮被点击以后调用更新状态的方法更新状态，
    			状态更新触发视图更新，渲染 state is changed
    		*/}
    		<p>{value}</p>
    		<button onClick={() => setValue("state is changed")}>更新视图状态</button>
    	</>
    )
}

export default App;
```
② 在函数组件中 useState 方法可以被调用多次用于声明多个组件状态

```react
import React, {useState} from "react";

function App() {
	const [value, setValue] = useState("initial state value");
	const [count, setCount] = useState(0);
	return (
		<>
			<p>{value}</p>
			<button onClick={() => setValue("state is changed")}>更新视图状态</button>
			<p>{count}</p>
			<button onClick={() => setCount(count + 1)}>+1</button>
			<button onClick={() => setCount(count - 1)}>-1</button>
		</>
	)
}

export default App;
```

③ 更新状态的方法也可以接收函数作为参数，通过参数函数的返回值指定新的状态值

```react
function App() {
	const [count, setCount] = useState(0);
	// prevState 表示更新前的状态
	// 参数函数的返回值表示更新后的状态
	return (
		<button onClick={() => setCount((prevState) => prevState + 1)}>{count}</button>
	)
}
```

```react
import React, {useState} from "react";

function App() {
	const [count, setCount] = useState(0);
	// 当多次调用 setCount 方法时，如果传递的是状态值，后面的状态值会覆盖前面的状态值
	// 所以当点击按钮时 count 每一次都会被 +2
	return (
		<button 
			onClick={() => {
				setCount(count + 1);
				setCount(count + 1);
				setCount(count + 1);
				setCount(count + 2);
			}}
		>
		{count}
		</button>
	)
}

export default App;
```

```react
import React, {useState} from "react";

function App() {
	// 当多次调用 setCount 方法时，如果传递的是函数，状态会被累加
	// 所以当点击按钮时 count 每一次都会被 +4
	const [count, setCount] = useState(0);
	return (
		<button 
			onClick={() => {
				setCount((prevState) => prevState + 1);
				setCount((prevState) => prevState + 1);
				setCount((prevState) => prevState + 1);
				setCount((prevState) => prevState + 1);
			}}
		>
			{count}
		</button>
	)
}

export default App;
// 虽然以上两段代码同时多次调用了修改状态的方法，但是状态不会被更新多次，只有当所以状态都得到最终的计算以后，才会一次更新视图。
```
④ 通过初始状态函数解决函数组件的性能问题

观察一下代码中存在的问题

```react 
import React, {useState} from "react";

function App() {
	let initialState = 0;
	for (let i = 0; i < 100000000; i++) {
		console.log(i);
		initialState += i;
	}
	const [number, setNumber] = useState(initialState);
	return (
		<button onClick={() => setNumber((prev) => prev + 1)}>{number}			</button>
	)
}

export default App;

// 在点击按钮时组件状态 number 会被更新，状态更新后为了重新渲染视图组件函数也会重新执行，每次组件函数重新执行时都会进行初始状态值的计算，但是初始状态值只在组件初始渲染时被用到，后续组件更新时是没有必要执行的。
```

```react
// 以上问题可以通过状态初始函数进行解决，初始状态函数只会在组件初始渲染时执行一次。
import React, { useState } from "react";

function App() {
  const [number, setNumber] = useState(() => {
    let initialState = 0;
    for (let i = 0; i < 10000; i++) {
      console.log(i);
      initialState += i;
    }
    return initialState;
  });
  return (
    <button onClick={() => setNumber((prev) => prev + 1)}>{number}</button>
  );
}

export default App;
```
⑤ 调用 useState 方法时的注意事项

在函数式组件中凡是以 use 开头的方法都只能在组件内部第一层作用域中调用

不能组件内部的其他方法中调用，不能在 if 条件判断中调用，不能在 for 循环中调用

```react
function App() {
  // ❎
  if (true) {
    const [count, setCount] = useState(0);
  }
	// ❎
  for (let i = 0; i < 5; i++) {
    const [count, setCount] = useState(0);
  }
	// ❎
  const onClickHandler = () => {
    const [count, setCount] = useState(0);
  };
  return <button onClick={onClickHandler}>{count}</button>;
}

```
##  3. 正确执行副作用 useEffect

**目标：掌握在函数组件中正确执行副作用代码的方式**

useEffect 方法的作用就是确保函数式组件中的副作用代码在正确的时机被执行。

① 什么是副作用代码

组件的职责是根据 Props 和 State 计算用户界面所需要的状态数据并渲染用户界面，其他得到和渲染用户界面没有关系的代码都属于副作用代码。

比如 Ajax Request、手动修改 DOM、本地存储、控制台输出、定时器等。

```react
// src/App.js
import React, {useState} from "react";

function App() {
	// 声明组件状态
	const [count, setCount] = useState(0);
	// 手动修改 DOM 对象  副作用代码
	document.title = count;
	// 控制台输出 副作用代码
	console.log("网页标题同步成功");
	// 渲染视图
	return <button onClick={() => setCount(count + 1)}>+1</button>
}

export default App;

```
② 避免副作用代码被重复执行

观察下列代码并说出代码中存在什么问题

```react
import React, {useState} from "react";

function App() {
	const [count, setCount] = useState(0);
	const [value, setValue] = useState(99);
	document.title = count;
	console.log("网页标题同步成功");
	return (
		<>
			<p>{count}</p>
			<button onClick={() => setCount(count + 1)}>+1</button>
			<button onClick={() => setValue(value - 1)}>{value}</button>
		</>
	)
}

export default App;
```

组件状态更新会引发组件函数重新执行，也就是说在以上代码中无论是count 还是 value ，只要发生更新组件函数就会重新执行。

但是组件中的副作用代码并不需要总是跟随组件更新而执行，只有 count 更新它才需要执行，而目前只要组件更新副作用代码就会执行。

那么如何保证副作用代码在正确的时机被执行呐？怎么保证以上组件中的副作用代码只在 count 状态发生变化执行呐？

使用 useEffect 方法监听特定状态的变化，当特定状态发生变化后在执行副作用代码。

```react
import {useEffect} from "react";

function App() {
	// useEffect 方法的第一个参数函数，该函数会在组件初始渲染时执行一次，会在监听的状态每次发生变化时执行。
	// useEffect 方法的第二个参数是数组，数组中填写的是依赖项发生变化会执行第一个参数函数
	useEffect(() => {}, [count])
}
```

**目标：通过 useEffect 监听 count 状态的变化, 只有在 count 状态发生变化以后才去执行更新网页标题的操作**

```react
import React, {useState, useEffect} from "react";

function App() {
	const [count, setCount] = useState(0);
	const [value, setValue] = useState(99);
	
	useEffect(() => {
		document.title = `useEffect方法的使用-${count}`;
		console.log("网页标题同步成功")
	}, [count]);
	return (
		<>
			<p>{count}</p>
			<button onClick={() => setCount(count + 1)}>+1</button>
			<button onClick={() => setValue(value - 1)}>{value}</button>
		</>
	)
}

export default App;
```

③ 组件代码执行顺序分析

useEffect 方法的参数函数是在视图渲染完成后执行的，这样做是为了避免副作用代码的执行阻塞用户界面的渲染。

```react
// 初始执行
// React: 返回 count 状态及更新该状态的 setCount 方法，返回 value 状态及修改状态的 setValue 方法
// App 组件: 把初始状态插入到视图模板中
// 浏览器: 根据 App 组件提供的视图模板渲染用户界面
// App 组件: 执行 useEffect 方法的第一个参数函数，即开始执行副作用代码
```
```react
// count 状态更新 
// 用户: 点击按钮更新了 count 状态
// React: 检测到 count 状态发生变化, 执行组件函数
// React: 返回最新的 count 状态及更新该状态的 setCount 方法、返回最新的 value 状态及修改该状态的 setValue 方法
// App 组件: 将最新的状态插入到组件模板中
// 浏览器: 根据 App 组件提供的新视图模板更新用户界面
// App 组件: 由于 count 状态发生变化, 执行 useEffect 方法的第一个参数函数, 即执行副作用代码
```
```react
// value 状态更新
// 用户: 点击按钮更新了 value 状态
// React: 检测到 value 状态发生变化, 执行组件函数
// React: 返回最新的 count 状态及更新该状态的 setCount 方法、返回最新的 value 状态及修改该状态的 setValue 方法
// App 组件: 将最新的状态插入到组件模板中
// 浏览器: 根据 App 组件提供的新视图模板更新用户界面
// App 组件: 由于 useEffect 依赖项 count 没有发生变化, 此次渲染之后不执行 useEffect 方法的第一个参数函数
```
④ 使用 useEffect 提供的清理函数消除副作用

只要 useEffect 的依赖项发生变化，useEffect 的第一个参数函数就会被执行，也就是说副作用代码可能会随组件更新而被执行多次。

在 JavaScript 中有些代码比如定时器，在开启新定时器之前就一定要清除老的定时器，否则多个定时器叠加执行会发生性能问题。

观察下列代码并指出代码中存在的问题

```react
import React, { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      console.log("启动定时器 -> " + id);
    }, 1000);
  }, [count]);

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

export default App;

```
在以上代码中存在的问题是只要 count 状态发生变化 useEffect 的参数函数就会执行，就会不断开启新的定时器导致多个定时器叠加执行。

那么开发者应该如何防止定时器叠加执行呢？

React 为开发者提供了清理函数，允许开发者在新的副作用代码执行前先清理旧的副作用代码。

```react
useEffect(() => {
	return () => {
		// 函数就是副作用代码的清理函数
		// 该函数会在新的副作用代码执行前执行，用于清理上一次的副作用代码
		// 组件初始渲染时只会执行 useEffect 方法的第一个参数函数，不会执行该清理函数，也没有必要执行，因为无内容可清理。
	}
}， [])
```
**目标：解决 App 组件中存在的定时器叠加执行的问题**

```react
import React, {useState, useEffect} from "react";

function App() {
	const [count, setCount] = useState(0);
	
	useEffect(() => {
		const id = setInterval(() => {
			console.log("启动定时器" + id);
		}, 1000);
		// 在每次执行副作用代码前先清理上一次副作用代码执行时开启的定时器
		return () => clearInterval(id);
	}, [count]);
	return <button onClick={() => setCount(count + 1)}>{count}</button>
}

export default App;

```
⑤ 组件代码执行顺序分析

```react
// 初始执行
// React: 返回 count 状态及更新该状态的 setCount 方法
// App 组件: 将初始状态插入到视图模板中
// 浏览器: 根据 App 组件提供的视图模板渲染用户界面
// App 组件: 执行 useEffect 方法的第一个参数函数, 即开启定时器 (初始执行, 不受依赖限制)

```
```react
// count 状态更新
// 用户: 点击按钮更新了 count 状态
// React: 检测到 count 状态发生变化, 执行组件函数
// React: 返回最新的 count 状态及更新该状态的 setCount 方法
// App 组件: 将最新的状态插入到组件模板中
// 浏览器: 根据 App 组件提供的新视图模板更新用户界面
// App 组件: 由于 count 状态发生变化, 执行清理函数, 清除上一次执行副作用代码时开启的定时器
// App 组件: 执行 useEffect 方法的参数函数, 执行新一轮组件渲染对应的副作用代码, 即开启一个新的定时器
```

⑥ 清理函数还会在组件卸载之前运行一次用于清理组件中的副作用

```react
import React, {useState, useEffect} from "react";
import {root} from "./index";

function App() {
	const [count, setCount] = useState(0);
	
	useEffect(() => {
		const id = setInterval(() => {
			console.log("启动定时器" + id);
		}, 1000)
		// 在每次执行副作用代码前先清理上一次副作用代码执行开启定时器
		return () => clearInterval(id);
	}, [count]);
	
	return (
		<>
			<button onClick={() => setCount(count + 1)}>{count}</button>
			<button onClick={() => root.unmount()}>卸载组件</button>
		</>
	)
}
export default App;
```
```react
// src/index.js
export const root =
ReactDOM.createRoot(document.getElementById("root"));
```

⑦ 使用useEffect 方法模拟组件初始渲染完成，即组件初始渲染完成后执行副作用代码

```bash
npm install axios@1.1.3
```

```react
import React, { useState, useEffect } from "react";
import axios from "axios";

function App() {
  const [user, setUser] = useState({});
  useEffect(() => {
    axios.get("https://api.github.com/users/defunkt").then((response) => {
      setUser(response.data);
    });
  }, []);
  return (
    <ul>
      <li>{user.name}</li>
      <li>{user.bio}</li>
      <li><img src={user.avatar_url} alt=""/></li>
    </ul>
  );
}

export default App;

```

##  4. 获取 DOM 对象 useRef

**目标：掌握使用 useRef 方法获取 DOM 对象的方式**

① 通过 useRef 方法可以在函数式组件中获取 DOM 对象

```react
import React, {useRef} from "react";

function App() {
	const username = useRef();
	return <input ref={username} onChange={() => 
		console.log(username.current)
	}/>
}

export default App;
```

② 通过 useRef 方法批量获取 DOM 对象

```react
import {useEffect, useRef, useState} from "react";

export default function App() {
	const [state] = useState(["a", "b", "c"]);
	const liRefs = useRef([]);
    useEffect(() => {
    	console.log(liRefs.current);
    }, []);
    return (
    	<ul>
    		{state.map((item, index) => (
    			<li ref={(element) => (liRefs.current[index] = element)} key = {item}>{item}</li>
    		))}
    	</ul>
    )
}
```

##  5. 获取子组件 DOM 对象 forwardRef

**目标：掌握通过 forwardRef 方法和 useRef 方法的配合使用可以获取子组件中的 DOM 对象**

forwardRef 是一个高阶函数。用于在父子组件之间传递 ref 对象，通过它可以实现获取子级组件中的 DOM 对象。

```react
// src/App.js
import React, {useRef, useEffect} form "react";
import Message from "./Message";

function App() {
	const spanRef = useRef();
	useEffect(() => {
		console.log(spanRef.current);
	}, []);
	return <Message ref={spanRef} />
}

export default App;
```

```react
// src/Message.js
import React, {forwardRef} from "react";

function Message(props, ref) {
	return <span ref={ref}>Hello React</span>
}

export default forwardRef(Message);
```

##  6. 受控表单组件

**目标：掌握在函数式组件中使用受控表单组件的方式**

```react
import React, {useState} from "react";

function App() {
	const [formState, setrFormState] = useState({
		username: "",
		password: "",
	});
	const onChangeHandler = (event) =>{
		setFormState({
			...formState,
			[event.target.name]: event.target.value,
		});
	};
	return (
		<>
			<input 
				type="text" 
				name="username" 
				value={formState.username} 
				onChange={onChangeHandler}
			/>
			<input 
				type="password"
				name="password"
				value={formState.password}
				onChange={onChangeHandler}
			/>
		</>
	)
}

export default App;
```

## 7. 非受控表单组件

**目标：掌握在函数组件中使用非受控表单组件的方式**

① 通过 useRef 方法实现非受控表单组件

```react
import React, {useRef} from "react";

function App() {
	const usernameRef = useRef();
	const onSubmitHandler = (event) => {
		event.preventDefault();
		console.log(usernameRef.current.value);
	};
	return (
		<form>
			<input type="text" ref={usernameRef}/>
			<input type="submit"/>
		</form>
	)
}

export default App;
```

##  8. 父子组件通讯 props

**目标：掌握函数式组件实现组件通讯的方式**

① 实现父组件传递状态到子组件，子组件修改父组件传递下来的状态值

```react
import React, {useState} from "react";

// 父组件
function App() {
	const [msg, setMsg] = useState("Hello React");
	// 把 msg 状态数据传递到子组件
	return <Message msg={msg} setMsg={setMsg} />
}

// 子组件
function Message(props) {
  // 接收来自父组件的 msg 状态数据
  return <button onClick={() => props.setMsg("message changed")}>{props.msg}</button>;
}

export default App;
```

② 设置 Props 对象默认值的方式

```react
import React from "react";

function App() {
	return <Message />
}

function Message({name, age}) {
	// 接收来自父组件的 msg 状态数据
	return (
		<div>{name} {age}</div>
	)
}

Message.defaultProps = {
	name: "王五",
	age: 60;
};

export default App;
```

```react
import Reat from "react";

function App() {
	return <Message name={"李四"} age={40} />;
}

function Message({name="张三", age=20}) {
	// 接收父组件的 msg 状态数据
	return (
		<div>
			{name} {age}
		</div>
	)
}

export default App;
```

##  9. 父子组件通讯 uselmperativeHandle

**目标：掌握通过 useImperativeHandle 方法实现父子组件通讯的方式**

useImperativeHandle 方法允许父组件直接调用子组件中暴露的成员属性和方法。

props 是父组件给，子组件要，useImperativeHandle 是是父组件要，子组件给。

```react
// src/App.js
import React, {useRef} from "react";

import Message from "./Message";

function App() {
	const msgRef = useRef();
	return (
		<>
			<Message ref={msgRef} />
			<button 
				onClick={() => {
					console.log(msgRef.current.value);
				}}
			>
				getMsg
			</button>
		</>
	)
}

export default App;
```

```react
// src/Message.js
import React, {forwardRef, useImperativeHandle, useState} from "react";

function Message(props, ref) {
	const [value, setValue] = useState("");
 	// useImperativeHandle 方法用于设置 ref 对象中的 current 属性的值
  	// 第一个参数传递 ref 对象
  	// 第二个参数传递函数, 函数返回什么, ref 对象中的 current 属性值就是什么, 该函数默认会在组件每次重新渲染时执行
  	// 第三个参数是一个数组, 传递依赖状态, 表示当依赖状态发生变化以后再执行第二个参数函数
	useImperativeHandle(ref, () => ({value}), [value]);
	return (
		<input 
			type="text"
			value={value}
			onChange={(event) => setValue(event.target.value)}
		/>
	)
}


export default forwardRef(Message);
```

## 10. 跨级组件通讯 useContext

**目标：掌握通过 useContext 方法获取 context 状态的方式**

{% asset_img 1.png This is an example image %}


```react
// src/index.js
import React, {createContext} from "react";
import ReactDOM from "react-dom/client";
import App from "./APP";

const root = ReactDOM.createRoot(document.getElementById("root"));
// 创建 context 上下文对象
export const PersonContext = createContext({name: "张三", age: 20});
// 通过 Provider 组件向下层组件开放状态
root.render(
	<PersonContext.Provider value={{name: "李四", age: 20}}>
		<App />
	</PersonContext.Provider>
)

```

```react
// src/App.js
import React from "react";
import Message from "./Message";

function App() {
  return <Message />;
}

export default App;

```

```reactr
// src/Message.js
import React, { useContext } from "react";
import { PersonContext } from "./index";

function Message() {
  // 使用 useContext 方法获取上下文状态
  const person = useContext(PersonContext);
  return <div>{person.name} {person.age}</div>;
}

export default Message;

```

##  11. 组件状态逻辑分离 useReducer

**目标：掌握使用 useReducer 方法管理组件状态的方式**

useReducer 方法是 React 提供的另一种在函数式组件中状态的方式

useReducer 方法的目标是把组件状态逻辑和组件渲染逻辑进行分离，使组件代码更加清晰可维护。

useReducer 方法的所有方式和 Redux 几乎相同，都需要尊从一套使用规则。

{% asset_img 2.png This is an example image %}

```react
// src/App.js
import React, {useReducer} from "react";
import counterReducer from "./counterReducer";

function App() {
	const [state, dispatch] = useReducer(counterReducer, {count: 0});
	return (
		<button onClick={() => dispatch({type: "counter/increment"})}>
			{state.count}
		</button>
	)
}

export default App;
```

```react
// src/counterReducer.js
export default function counterReducer(state, action) {
	switch (action.type) {
		case "counter/increment";
			return {
				...state,
				count: state.count + 1,
			}；
		default:
			return state;
	}
}

```

##  12. 保存组件值 useRef

**目标：掌握使用 useRef 保存值的方式**

useRef 除了可以获取 DOM 元素以外，还可以保存普通值。

使用 useRef 保存的普通值不会随组件更新而销毁，修改通过 useRef 保存的值也不会触发组件更新。

需求一：记录组件更新次数。

```react
import {useEffect, useRef, useState} from "react";

export default function App() {
	// 记录组件被渲染的次数
	const ref = useRef({renderCount: 0});
	// 记录用户在文本框中输入的值
	const [value, setValue] = useState("");
	// 组件每次渲染时执行
	useEffect(() => {
		ref.current.renderCount += 1;
		console.log(ref.current.renderCount);
	});
	return (
		<input type="text" value={value} onChange={(event) => setValue(event.target.value)} />
	);
}
```

需求二：组件初次渲染完成后开启定时器，点击按钮时清空定时器。

```react
import {useEffect, useRef, useState} from "react";

export default function App() {
	// 用于测试组件不断重新渲染后，useRef 保存的值仍在
	const [count, setCount] = useState(0);
	// 用于保存定时器 id
	const intervalRef = useRef();
	// 组件初次渲染时执行
	useEffect(() => {
		// 开启定时器 保存定时器 id
		intervalRef.current = window.setInterval(() => {
			console.log("定时器")
		}, 1000);
		// 组件卸载时清理定时器
		return () => clearInterval(intervalRef.current);
	}, []);
	return (
		<>
			<button onClick={() => clearInterval(intervalRef.current)}
			>清除定时器<button/>
			><button onClick={() => setCount((prev) => prev + 1)}
			>{count}<button/>
		</>
	)

}
```

##  13. 组件性能优化 memo

**目标：掌握使用 memo 方法优化组件运行性能的方式**

memo 是 React 为函数式组件提供的用于优化组件运行性能的方法。

memo 方法可以对组件输入数据进行浅层比较，如果输入数据没有变化则阻止组件更新。

```react
import React, {useState, useEffect} from "reacct";
import Message from "./Message";

function App() {
	const [person, setPerson] = useState({name: "张三", age: 20});
	useEffect(() => {
		let timer = setInterval(() => {
			setPerson({...person, age: person.age + 1});
		}, 1000);
		return () => clearInterval(timer);
	}, [person]);
	return (
		<>
			<div>{person.age}</div>
			<Message name={person.name} />
		</>
	)
}

export default App;
```

```react
import React, {memo} from "react";

function Message({name}) {
	console.log("Message render");
	return <div>{name}</div>
}

export default memo(Message);
```
memo 方法默认只能进行浅层比较，对于引用数据类型仅比较内存中的引用地址。

```react
// 虽然 p1 和 p2 的值完全相同, 但是它们在内存中的引用地址不一样, 所以它们不相等。
var p1 = {name: "张三"};
var p2 = {name: "张三"};
// false
p1 === p2
```
React 组件输入数据经常会遇到以上问题导致组件重新渲染，虽然输入数据的值本身并没有变化。

为了解决以上问题，memo 方法提供了第二个参数即自定义比较函数，通过它可以控制组件是否响应更新。

自定义比较函数要求返回布尔类型的值，true 表示阻止更新，false 表示允许更新。

自定义比较函数接收两个参数，第一个参数是上一次更新时使用的输入数据，第二个参数是最新一次更新时使用过的输入数据。

```react
import React, {useState, useEffect} from "react";
import Message from "./Message";

function App() {
	const [person, setPerson] = useState({name: "张三", age: 20});
	useEffect(() => {
		let timer = setInterval(() => {
			setPerson({...person, age: person.age + 1});
		}, 1000);
		return () => clearInterval(timer);
	}, [person]);
	return (
		<>
			<div>{person.age}</div>
			<Message person={person} />
		</>
	)
}

export default App;
```

```react
import React, {memo} from "react";

function Message({person}) {
	console.log("Message render");
	return <div>{person.name}</div>
}

export default memo(Message, (prevProps, nextProps) => prevProps.name === nextProps.name);
```
##  14. 组件性能优化 useMemo

**目标：掌握 useMemo 方法的使用方式**

useMemo 方法用于在函数式组件中缓存值，以避免不必要的资源密集型操作重复执行影响组件运行性能。

```react
import React, {useState, useMemo} from "react";

function App() {
	const [count, setCount] = useState(0);
	const [dark, setDark] = useState(false);
	
	const multiple = useMemo(() => {
		return count + 2;
	}, [count]);
	return (
		<>
			<button onClick={() => setCount(count + 1)}>{count} - {multiple}</button>
			<button onClick={() => setDark(!dark)}>{dark ? "dark": "light"}</button>
		</>
	)
}

export default App;
```

##  15. 组件性能优化 useCallback

**目标：掌握 useCallback 方法的使用方式**

useCallback 方法用于在函数式组件中缓存方法，以避免组件在每次重新渲染时都返回一个新的方法。

```react
import React, {useState, useMemo, useCallback} from "react";
import List from "./List";

function App() {
	const [count, setCount] = useState(0);
	const [dark, setDark] = useState(false);
	
	const getItems = useCallback(() => {
		return [count, count + 1, count + 2];
	}, [count]);
	return (
		<>
			<List getItems={getItems}/>
			<button onClick={() => setCount(count + 1)}>button</button>
			<button onClick={() => setDark(!dark)}>{dark ? "dark" : "light"}</button>
		</>
	)
}

export default App;
```

```react
import React, {memo} from "react";

function List(props) {
	return <ul>{props.getItems().map((item) => <li key={item}>{item}</li>)}</ul>
}

export default memo(List);
```
useEffect 与异步函数

开发者经常会在 useEffect 中执行异步操作比如发送 Ajax 请求，和异步操作相关联的最密切的当属异步函数，先观察以下代码。

```react
useEffect(async () => {
	const data = await fetchData();
}, [fetchDate]);

```

以上代码是错误的写法，useEffect 方法的第一个参数不能是异步函数，因为 useEffect 期望该参数函数要返回 undefined 要么返回清理函数。

而异步函数返回 Promise 对象，不符合 useEffect 的要求，正确的做法如下。

```react
export default function App{
	const fetchData = useCallback(async () => {
		const data = await fetchData();
	}, []);
	useEffect(() => {
		fetchDate();
	}, [fetchDate])
}

```

需求：在页面中准备两个按钮，点击按钮时获取用户信息并渲染。

```react
import React, {useState, useEffect, useCallback} from "react";
import axios from "axios";

export default function App() {
	const [user, seyUser] = useState({});
	const [name, setName] = useState("defunkt");
	
	const fetchUser = useCallback(async() => {
		let response = await axios.get
			(`https://api.githun.com/users/${name}`);
		setUser(response.data)
	}, [name]);
	useEffect(() => {
		fetchUser();
	}, [fetchUser]);
	return (
		<div>
			<button onClick={() => setName("Starstruck")}>Starstruck</button>
			<button onClick={() => 
setName("likethesky")}>likethesky</button>
			<ul>
				<li>{user.name}</li>
				<li>{user.bio}</li>
				<li>
					<img src={user.avatar_url} alt="" />
				</li>
			</ul>
		</div>
	)
}

```

##  16. 组件性能优化 useDeferredValue

**目标：掌握在函数式组件中使用 useDeferredValue 方法的方式**

通过 useDeferredValue 方法可以获取到一个延迟更新的值，即在 React 空闲时在去更新的值。

在需要频繁更新视图得到场景下可以避免视图出现卡顿现象，使应用程序更新流畅，增强用户体验。

```react
import React, {useState} from "react";
import List from "./List"

function App() {
	const [value, setValue] = useState("");
	return (
		<>
			<input
            	type="text"
            	value={value}
            	onChange={(event) => setValue(event.target.value)}
            />
            <List value={value} />
		</>
	)
}

export default App;

```
```react
import React, {useDeferredValue, useMemo} from "react";

function List({value}) {
	const deferredValue = useDeferredValue(value);
	const list = useMemo(() => {
		let values = [];
		for (let i = 0; i < 10000; i ++) {
			values.push(<div key={i}>{value}</div>)
		}
		return values;
	}, [deferredValue]);
	return list;
}

export default List;
```

##  17. 组件性能优化 useTransition

**目标：掌握在函数式组件中使用 useTransition 方法的方式**

useTransition 方法允许开发者调整状态渲染的优先级。

开发者可以使用 useTransition 方法把资源密集型任务的渲染优先级降低待 React 空闲时在执行，避免页面出现卡顿现象。

```react
import React, {useState, useTransition} from "react";

function App () {
	const [value, setValue] = useState("");
	const [list, setList] = useState([]);
	const [isPending, startTransition] = useTransition();
	const onChangeHandler = (event) => {
		setValue(event.target,value);
		startTransition(() => {
			let values = [];
			for (let i = 0; i < 10000; i ++) {
				values.push(<li key={i}>{event.target.value}</li>)
			}
			setList(values);
		})
	};
	return (
		<>
			<input type="text" value={value} onChange={onChangeHandler}/>
			{isPending ? <div>loading...</div> : <ul>{list}</ul>}
		</>
	)
}

export default App;

```

##  18. 自定义 Hook 训练 useLocalStorage

**目标：创建自定义构子函数 useLocalStorage 用于把组件状态实时同步到本地存储 localStorage**

React 允许开发者创建自定义构子函数以扩展函数组件的功能。

自定义构子函数其实就是应用逻辑和内置钩子函数的组合。

```react
import {useState} from "react";

export function useLocalStorage(key, initialValue) {
	// 声明状态
	const [storedValue, setStoredValue] = useState(function () {
		// 看本地是否存在已有状态值
		const item = window.localStorage.getItem(key);
		// 如果本地已经有就用本地的
		if (item) {
			return JSON.parse(item);
		} else {
			// 把初始值存储到本地
			window.localStorage.setItem(key, JSON.stringify(initialValue));
			// 本地没有使用初始值
			return initialValue;
		}
	});
	// 对设置状态的方法进行增强 添加状态同步到本地存储的功能
	const setState = (value) => {
		// 获取新的状态值
		// 如果 value 是函数类型 调用函数传递现有状态 从返回值中获取新的状态
		// 如果 value 是其他类型 直接作为状态值使用
		const valueToStore = value instanceof Function ? value(storedValue) : value;
		// 设置状态
		setStoredValue(valueToStore);
		// 把状态值同步到 localStorage
		localStorage.setItem(key, JSON.stringify(valueToStore));
	};
	// 返回状态及设置状态的方法
	return [storedValue, setState];
}
 
```

```react
import React from "react";
import {useLocalStorage} from "./useLocalStorage";

function App() {
	const [count, setCount] = useLocalStorage("count", 0);
	return <button onClick={() => setCount(count + 1)}>{count}</button>
}

export default App();
```

##  19. 自定义 Hook 训练 useToggle

**目标：创建自定义钩子函数 useToggle 用于返回布尔值状态及切换布尔值状态的方法**

```react
import {useCallback, useState} from "react";

export default function useToggle(initialValue = false) {
	const [state, setState] = useState(initialValue);
	const toggle = useCallback(() => {
		setState((state) => !state);
	}, []);
	return [state, toggle];
}

```

```react
import React from "recat";
import useToggle from "./useToggle";

function App() {
	const [isToggle, toggle] = useToggle(false);
	return <button onClick={toggle}>{isToggle ? "world" : "Hello"}</button>
}

export default App;
```

##  20. 自定义 Hook 训练 useRequest

**目标：创建自定义钩子函数 useRequest 用于发送请求**

```react
import axios from "axios";
import {useCallback, useEffect, useState} from "react";

export default function useRequest(conf) {
	const [config, setConfig] = useState(conf);
	// 和请求相关的状态
	const [{data, status, error}, setState] = useState({
		// 请求结果
		data: null,
		// 请求状态
		status: "idle",
		// 错误信息
		error: null,
	});
	// 用于发送请求的方法
	const request = useCallback(() => {
		// 更新请求状态
		setState({data: null, status: "pending", error: null});
		// 发送请求
		axios
			.request(config)
			.then((response) => {
				// 请求成功 保存状态
				setState({ data: response.data, status: "success", error: null });
			})
			.catch((error) => {
        	// 请求失败
        	setState({ data: null, status: "error", error: error.message});
	}, [config]);
	// 监控请求方法是否发生改变
	useEffect(() => {
		// 重新发送请求
		request();
	}, [request]);
	// 返回钩子函数外部需要的状态
	return {data, status, error, config, setConfig};
}
```

```react
import React from "react";
import useRequest from "./useRequest";

function App() {
	const {status, data, error, setConfig} = useRequest({
		url: "https://jsonplaceholder.typicode.com/todos/1",
	});
	
	let jsx;
	if (status === "idle") jsx = null;
	if (status === "pending") jsx = <div>加载中...</div>
	if (status === "error") jsx = <div>{error}</div>
	if (status === "success") jsx = <div>{JSON.stringify(data)}</div>
	
	// 用于修改请求参数 重新获取数据的方法
	const onRequest = () => {
		// 随机生成 1- 100 之间的数值作为 id
		const id = Math.ceil(Math.random() * 100);
		// 更新请求参数
		setConfig({
			url: `https://jsonplaceholder.typicode.com/todos/${id}`
		});
	};
	return (
		<>
			<button onClick={onRequest}>button</button>
			{jsx}
		</>
	)
}

export default App;
```

## 21. 自定义 Hook 训练 useHover

**目标：创建自定义钩子函数 useHover 用于检测鼠标是否移入移出了某一个元素**

```react
import {useEffect, useRef, useState} from "react";

export default function useHover() {
	const [value, setValue] = useState(false);
	const elementRef = useRef();
	
	useEffect(() => {
		const node = elementRef.current;
		if (!node) return;
		const handleMouseEnter = () => setValue(true);
		const handleMouseLeave = () => setValue(false);
		node.addEventListener("mouseenter", handleMouseEnter);
		node.addEventListener("mouseleave", handleMouseLeave);
		return () => {
			node.removeEventListener("mouseenter", handleMouseEnter);
			node.removeEventListener("mouseleave", handleMouseLeave);
		}
	}, []);
	return [elementRef, value];
}
```

```react
import React from "react";
import useHover from "./useHover";

function App() {
	const [elementRef, isHover] = useHover();
	return <div ref={elementRef}>{isHover ? "😁" : "☹️"}</div>
}

export default App;
```

##  22. 自定义 Hook 训练 useWindowSize

**目标：创建自定义钩子函数 useWindowSize 用于获取浏览器窗口大小**

```react
import {useEffect, useState} from "react";

export default function useWindowSize() {
	const [windowSize, setWindowSize] = useState({
		width: undefined,
		height: undefined,
	});
	useEffect(() => {
		const handleResize = () => {
			setWindowSize({
				width: window.innerWidth,
				height: window.innerHeight,
			});
		};
		window.addEventListener("resize", handleResize);
		handleResize();
		return () => window.removeEventListener("resize", handleResize);
	}, []);
	return windowSize;
}
```
```react
import React from "react";
import useWindowSize from "./useWindowSize";

function App() {
	const size = useWindowSize();
	return <div>{size.width}px / {size.height}px</div>
}

export default App;
```















