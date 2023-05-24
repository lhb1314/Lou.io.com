---
title: React-TypeScript-函数组件
date: 2023-04-25 15:05:08
tags:
top_img: https://www.linuxprobe.com/wp-content/uploads/2016/10/0-react01-1.jpg
cover: https://www.linuxprobe.com/wp-content/uploads/2016/10/0-react01-1.jpg
---

# React-TypeScript-函数组件

## 1. 创建应用

**目标：掌握创建 React 应用的方式（支持 TypeScript）**

使用 React 官方提供的 create-react-app 脚手架工具即可创建支持 TypeScript 的 React 应用。

我们只需要在命令中添加 --template typescript 选项即可创建 TypeScript 项目。

```bash
mkdir react-ts-tutorial && cd react-ts-tutorial && code .
create-react-app ./ --template typescript
```
在 TypeScript 项目中包含 JSX 代码的文件后缀名称为 tsx，其他不包含 JSX 代码的文件后缀名称为 ts。

```tsx
// src/App.tsx
export default function App() {
  return <div>App</div>;
}
```

## 2. 为函数组件标注类型

**目标：掌握为函数组件标注类型的方式**

```react
// src/App.tsx
export default function App(): JSX.Element {
	return <div>App Works</div>
}
```

```react
// src/App.tsx
import {FC} from "react";

const App: FC = () => {
	return <div>App Works</div>
};

export default App;
```

##  3. 标注 Props 对象的类型

**目标：掌握标注函数组件 Props 对象的类型**

```tsx
// src/App.tsx
interface Props {
	name: string;
}

export default function App(props: Props): JSX.Element {
	return <div>{props.name}</div>
}
```

```tsx
// src/index.tsx
root.render(<App name="张三" />);
```

```tsx
// src/App.tsx
import {FC} from "react";

interface Props {
	name: string
}

const App: FC<Props> = (props) => {
	return <div>{props.name}</div>
};

export default App;
```

##  4. 标注 useState 状态类型

**目标：掌握标注状态类型的方式（通过 useState 方法创建）**

① 在声明状态时如果状态有初始值不需要显式标注状态类型使用 TypeScript 中的类型推断即可

```react
import {useState} from "react";

export default function App() {
	const [state, setState] = useState(0);
	
	return (
		<>
			<button onClick={() => setState(state + 1)}>{state}</button>
			<button onClick={() => setState((prev) => prev + 1)}>{state}</button>
		</>
	)
}
```

② 对于不能使用类型推断的场景可以使用泛型参数标注状态的类型

```tsx
import {useState} from "react";

export default function App() {
	const [state, setState] = useState<number[]>([]);
	return (
		<>
			<button onClick={() => setState((prev) => [...prev, Math.random()])}>add</button>
			<ul>
				{state.map((item) => (
					<li key={item}>{item}</li>
				))}
			</ul>
		</>
	)
}
```

## 5. 标注 useReducer 状态类型

**目标：掌握标注状态类型的方式（通过 useReducer 方法创建）**

```react
import {useReducer} from "react";

const initialState: CounterState = {
	count: 0,
};

interface CounterState {
	count: number;
}

type CounterActions = 
	{type: "counter/increment"} |
	{type: "counter/decrement"} |
	{type: "counter/incrementByCoount"; payload: {count: number}};
	
function counterReducer(state: CounterState, action: CounterActions):
	CounterState {
		switch(action.type) {
			case "counter/increment":
				return {count: state.count + 1}
			case "counter/decrement":
				return {count: state.count - 1}
			case "counter/incrementByCount":
				return {count: state.count + action.payload.count}
		}	
	}
	
	export default function App() {
		const [state, dispatch] = useReducer(counterReducer, initialState);
		return (
			<>
				{state.count}
				<button onClick={() => disoatch({type: "counter/increment"})}>+1</button>
				<button onClick={() => disoatch({type: "counter/decrement"})}>-1</button>
				<button onClick={() => disoatch({type: "counter/incrementByCount", payload: {count: 10}})}>+10</button>
			</>
		)
	}
```

## 6. 标注 useRef 状态类型

**目标：掌握标注状态类型的方式（通过 useRef 方法创建）**

```react
import {useEffect, useRef} from "react";

export default function App() {
	// 注意: 默认值必须是 null
	// 因为在 javaScript 中 获取元素的方法的返回值在没有获取元素时返回值都是 null
	const buttonRef = useRef<HTMLButtonElement>(null);
	// 组件初次渲染完成后
	useEffect(() => {
		// 检测是否获取到 button 元素
		if (!buttonRef.current) return;
		// 测试输出 button 元素
		console.log(buttonRef.current);
	}, []);
	// 渲染视图 获取 button 元素
	return <button ref={buttonRef}>button</button>;
}
```

## 7. 标注 forwardRef 方法类型

**目标：掌握在调用 forwardRef 方法时为其传递泛型参数的方式**

```react
// src/Message.tsx
import {forwardRef, useImperativeHandle} from "react";

export interface MsgRef {
	msg: string;
}

interface MsgProps {
	test: string;
}

// 1. 定义 forwardRef 方法返回组件调用时接收的 ref 属性值得类型
// 2. 定义 forwardRef 方法返回组件调用时接收的 props 对象的类型
// forwardRef 会把接收到的 ref 和 props 传递给我们定义的组件
const Message = forwardRef<MsgRef, MsgProps>((props, ref) => {
	// 为 ref 对象赋值 值必须符合 MsgRef 类型
	useImperativeHandle(ref, () => ({msg: "hello"}));
	return <div>{props.test}</div>
});

export default Message;
```
```tsx
// src/App.tsx
import {useEffect, useRef} from "react";
import Message, {MsgRef} from "./Message";

export default function App() {
	const ref = useRef<MsgRef>(null);
	useEffect(() => {
		console.log(ref.current?.msg);
	}, []);
	return <Message ref={ref} test="test" />
}
```

##  8. 配置 Redux Toolkit

**目标：在支持 TypeScript 的 React 应用中配置 Redux Toolkit**

```bash
# 该包自带类型声明文件 不需要单独下载
npm i @reduxjs/toolkit@1.9.0 react-redux@8.0.5
```

```tsx
// src/store/index.ts
import {configureStore} from "@reduxjs/toolkit";
// 创建 store 对象
export const store = configureStore({
	devTools: process.env.NODE_ENV !== "production",
	reducer: {},
});
```
```tsx
// src/index.tsx
import {Provider} from "react-redux";
import {store} from "./store";

// 配置 Provider 组件
root.render(
	<Provider store={store}>
		<App />
	</Provider>
)
```

## 9. createAction

**目标：掌握在创建 action creator 函数时标注 action payload 参数的类型**

```ts
// src/store/creators/counterCreators.ts
import {createAction} from "@reduxjs/toolkit";

export const increment = createAction("counter/increment");
export const incrementByCount = createAction<{count: number}>("counter/incrementByCount");

// incrementByCount({count: 10});
```

## 10. createReducer

**目标：掌握在创建 reducer 函数时标注状态的方式**

```tsx
// src/store/reducers/counterReducer.ts
import {createReducer} from "@reduxjs/toolkit";
import {increment, incrementByCount} from "../creators/counterrCreators";

// reducer 函数操作的状态的类型
export interface CounterState {
	count: number
}

// 初始状态
const initialState: CounterState = {
	count: 0,
};

// 创建 reducer 函数
const counterReducer = createReducer<CounterState>(initialState, (builder) => {
	builder
		.addCase(increment, (state) => ({count: state.count + 1}))
		.addCase(incrementByCount, (state, action) => ({count: state.count + action.payload.count}))
		.addDefaultCase((state) => state);
});

export default counterReducer;
```

```tsx
// src/store/index.ts
import counterReducer from "./reducers/counterReducer";

export const store = configursStore({
	reducer: {
		counterReducer,
	}
})
```
##  11. useSelector

**目标：掌握在组件中通过 useSelector 获取状态时标注 Redux Store 状态对象的类型和要获取的状态的类型**

① 为 useSelector 方法设置类型的方式

```tsx
// src/components/Counter.tsx
import {useSelector} from "react-redux";
import {AppState} from "../store";
import { CounterState } from "../store/reducers/counterReducer";

export default function Counter() {
	const counterReduer = useSelector<AppState, CounterState>((state) => state.counterReducer);
	return <div>{counterReducer.count}</div>;
}

```

```tsx
// src/store/index.ts
// 声明 Redux Store 中状态对象的类型
export type AppState = ReturnType<typrof store.getState>;
```