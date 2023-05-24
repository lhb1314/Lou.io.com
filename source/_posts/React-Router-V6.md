---
title: React Router V6
date: 2023-04-24 14:40:47
tags:
top_img: https://oss-cn-hangzhou.aliyuncs.com/codingsky/cdn/img/2021-07-30/75adf9c0aa068854f5ff11cd558c0647
cover: https://oss-cn-hangzhou.aliyuncs.com/codingsky/cdn/img/2021-07-30/75adf9c0aa068854f5ff11cd558c0647
---

#  React Router V6

##  1. 集成路由功能

**目标：掌握在 React 应用中集成 React Router V6 的方式**

使用 create-react-app 5.0.1 创建新的基于 React 18.2.0 的应用并在应用中安装 React Router V6

在应用中集成 React Router V6 路由系统

① 使用 create-react-app 5.0.1 创建新的基于 React 18.2.0 的应用并在应用中安装 React Router V6

```bash
# 创建 react-router-tutorial 目录
mkdir react-router-tutorial
# 使用 VSCode 打开当前目录
code .
# 在当前目录中创建 react 应用
react-react-app ./
# 在应用中安装路由库
npm install react-router-dom@6.4.3
```

② 在应用中集成 React Router V6 路由系统 

```react
// src/index.js
import React from "react";
import ReactDOM from "react-dom/client";
// createBrowserRouter 用于创建基于浏览器历史记录的路由系统
// RouterProvider 用于配置路由系统的组件
import {createBrowserRouter, RouterProvider} from "react-router-dom";
// 创建路由系统
const router = createBrowserRouter([
	// 当用户在浏览器中访问 / 路径时 渲染 
	{
		path: "/",
		element: <div>Hello React Router DOM V6</div>
	}
]);
const root = ReactDOM.createRoot(document.getElementById("root"));
// 使路由规则生效
root.render(<RouterProvider router={router} />);

```

##  2. 配置路由组件

**目标：创建首页页面组件和专题页面组件并配置其对应的路由规则**

创建首页页面组件和专题页面组件
配置以上两个页面组件对应的路由规则

① 创建首页页面组件和专题页面组件
```react
// src/pages/home/index.js
import React from "react";

export default function HomePage() {
	return <div>首页页面</div>
}
```

```react
// src/pages/topic/index.js 
import React from "react";

export default function TopicPage() {
	return <div>专题页面</div>
}
```

② 配置以上两个页面组件对应的路由规则

```react
// src/index.js
import HomePage from "./pages/home";
import TopicPage from "./pages/topic";

// 注意在 v6 版本中 请求路径 不在需要使用 exact 属性
const router = createBrowSerRouter([
	// 当用户在浏览器中访问 路径时 渲染 homepage 组件
	{
		path: "/",
		element: <HomePage />
	},
	// 当用户在浏览器中访问 topic 路径时 渲染 topicpage 组件
	{
		path: "/topic",
		element: <TopicPage />
	}
])
```

## 3. 配置嵌套路由

**目标：掌握创建嵌套路由的方式**

需求：创建新闻页面作为一级路由，创建公司新闻和行业新闻页面为二级路由。

创建新闻页面组件 公司新闻组件 行业新闻组件
配置新闻组件 公司新闻组件 行业新闻组件对应的路由规则
在一级路由新闻页面组件中添加占位符组件使子级路由组件有渲染位置

① 创建新闻页面组件 公司新闻组件 行业新闻组件

```react
// src/pages/news/index.js
import React from "react";

export default function NewsPage() {
	return <div>新闻页面</div>
}
```
```react
// src/pages/news/company/index.js
import React from "react";

export default function CompanyNewsPage() {
	return <div>公司新闻</div>
}
```
```react
// src/pages/news/industry/index.js
import React from "react";

export default function IndustryNewsPage() {
	return <div>行业新闻</div>
}
```

② 配置新闻组件 公司新闻组件 行业新闻组件对应的路由规则

```react
// src/index.js
import NewsPage from "./pages/news";
import CompanyNewsPage from "./pages/news/company";
import IndustryNewsPage from "./pages/news/industry";

const router = createBrowserRouter([
	// 当用户在浏览器中访问 news 路径时 渲染 newspage 组件
	{
		path: "/news",
		element: <NewsPage />,
		children: [
			// 当用户在浏览器中访问 news/company 路径时 把 companynewspage 组件渲染到 newspage 组件中
			{
				path: "company",
				element: <companynewspage />
			},
			{
				path: "industry",
				element: <industrynewspage />
			}
		],
	},
]);
```

③ 在一级路由新闻页面组件中添加占位符组件使子级路由组件有渲染位置

```react
// src/pages/news/index.js
import {Outlet} from "react-router-dom";

export default function newspage() {
	// 子路由页面组件把会被渲染到占位符组件所在的位置
	return <Outlet />
}
```

## 4. 配置布局组件

**目标：掌握在应用中通过路由配置布局组件的方式**

创建布局组件并使用 Outlet 组件指定子级路由组件的渲染位置
配置布局组件及页面组件的路由规则使布局组件和页面组件组合成完整的页面结构

① 创建布局组件并使用 Outlet 组件指定子级路由组件的渲染位置

```react
// src/shared/layout/index.js
import React from "react";
import {Outlet} from "react-router-dom";s

export default function Layout() {
	return (
		<>
			<div>Layout 布局组件</div>
			<Outlet />
		</>
	)
}
```

② 配置布局组件及页面组件的路由规则使布局组件和页面组件组合成完整的页面结构

```react
// src/index.js
import Layout from "./shared/layout";

const routrer = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			{
				path: "",
				element: <HomePage />
			},
			{
				path: "news",
				element: <NewsPage />,
				children: [
					{
						path: "company",
						element: <CompanyNewsPage />
					},
					{
						path： "industry",
						element: <IndustryNewsPage />
					}
				]
			}
		]
	}
])
```

##  5. 配置导航链接

**目标：掌握在应用中配置导航链接的方式**

创建 Navigation 组件并在其中通过 Link 组件渲染导航链接
通过 NavLink 组件渲染导航链接
更改 Router Router 为激活的链接添加的默认激活类名

① 创建 Navigation 组件并在其中通过 Link 组件渲染导航链接

通过 Link 组件生成的链接在被激活时 React Router 并不会为其添加激活类名。

```react
// src/shared/navigation/index.js
import React from "react";
import {Link} from "react-router-dom";

export default function Navigation() {
	return (
		<div>
			<Link to="/">首页</Link>
			<Link to="/topic">专题</Link>
			<Link to="/news">新闻</Link>
		</div>
	);
}
```
```react
// src/shared/layout/index.js
import Navigation from "../navigation";

export default function Layout() {
	return (
		<>
			<Navigation />
		 	<Outlet />
		</>
	)
}
```

② 通过 NavLink 组件渲染导航链接

通过 NavLink 组件生成的链接在被激活时 React Router 会为其添加激活类名 默认激活类名为 active

```react
// src/shared/navigation/index.js
import React from "react";
import {NavLink} from "react-router-dom";

export default function Navigation() {
	return (
		<div>
			<NavLink to="/">首页</NavLink>
			<NavLink to="/topic">专题</NavLink>
			<NavLink to="/news">新闻</NavLink>
		</div>
	)
}
```
```react
// src/pages/news/index.js
import {Outlet, NavLink} from "react-router-dom";

export default function NewsPage() {
	return (
		<div>
			<NavLink to="/news/company">公司新闻</NavLink>
			<NavLink to="/news/industry">行业新闻</NavLink>
			<Outlet />
		</div>
	)
}
```

③ 更改 Router Router 为激活的链接添加的默认激活类名

```react
// src/shared/navigation/index.js

// 当前函数的返回值即是链接激活时被添加的类名
// isActive 参数为布尔值 链接被激活时值为 true 链接未激活时值为 false
const activeClassName = ({isActive}) => (isActive ? "selected" : "");

export default function Navigation() {
	return (
		<div>
			{/*
				NavLink 组件的 className 属性的值可以是一个函数
				通过函数参数可以知道该链接是否被激活
				通过函数返回值告诉 React Router 链接激活时添加的类名是什么
			*/}
			<NavLink to="/" className={activeClassName}>首页</NavLink>
			<NavLink to="/topic" className={activeClassName}>专题</NavLink>
			<NavLink to="/news" className={activeClassName}>新闻</NavLink>
		</div>
	)
}
```

##  6. 路由路径参数

**目标：掌握在组件中获取路由路径参数的方式**

需求：创建关于我们页面组件 进入该页面时需要传递团队名称作为参数 当进入到该页面组件后获取路由路径参数并渲染团队名称

1. 创建团队简介页面组件
2. 配置团队简介页面组件对应的路由规则
3. 在首页页面组件中添加团队简介页面链接
4. 在团队简介页面组件中获取路由参数

① 创建团队简介页面组件

```react
// src/pages/team/index.js
import React from "react";

export default function Team() {
	return <div>团队简介页面</div>
}
```

② 配置团队简介页面组件对应的路由规则

```react
// src/index.js
import TeamPage from "./pages/team";

const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			// 当用户在浏览器中访问 team 团队名称 路径时 渲染 team 组件
			{
				path: "team/:name",
				element: <teampage />
			}
		]
	}
])

```

③ 在首页页面组件中添加团队简介页面链接

```react
// src/pages/home/index.js
import {Link} from "react-router-dom";

export default function homepage() {
	return (
		<div>
			首页页面
			<ul>
				<li>
					<Link to="/team/team-a">team a</Link>
				</li>
				<li>
					<Link to="/team/team-a">team a</Link>
				</li>
			</ul>
		</div>
	)
}

```

④ 在团队简介页面组件中获取路由参数

```react
// src/pages/team/index.js
import {useParams} from "react-router-dom";

export default function teampage() {
	const {name} = useParams();
	return <div>团队介绍页面 {name}</div>
}

```
## 7. 路由查询参数

**目标：掌握在组件中获取路由查询参数的方式**

1. 创建登录页面路由组件
2. 配置登录页面路由组件的路由规则
3. 在首页页面组件中添加用于跳转到登录页面的链接
4. 在登录页面组件中获取路由查询参数

① 创建登录页面路由组件

```react
// src/pages/login/index.js
import React from "react";

export default function LoginPage() {
	return <div>登录页面</div>;
}

```

② 配置登录页面路由组件的路由规则

```react
// src/index.js
import LoginPage from "./pages/login";

const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			// 当用户在浏览器中访问 login 路径时 把 loginpage 组件渲染到 layout 组件中
			{
				path: "login",
				element: <LoginPage />
			}
		]
	}
])

```

③ 在首页页面组件中添加用于跳转到登录页面的链接

```react
// src/pages/home/index.js
export default function HomePage() {
	return (
		<p>
			<Link to="/login?returnUrl=testUrl">登录</Link>
		</p>
	)
}
```

④ 在登录页面组件中获取路由查询参数

```react
// src/pages/login/index.js
import React from "react";
import {useSearchParams} from "react-router-dom";

export default function LoginPage() {
	// 获取路由查询参数操作对象
	const [searchParams] = useSearchParams();
	// 获取路由参数 returnUrl 的值
	const returnUrl = searchParams.get("returnUrl");
	// 渲染视图
	return <div>登录页面 {returnUrl}</div>
}
```

## 8. 创建路由守卫

**目标：掌握在React Router V6 中实现路由守卫的方式**

当用户去访问哪些需要鉴权以后才能进入的路由组件时 需要先通过路由守卫对其进行鉴权 只有通过才允许用户进入 否则进行重定向

1. 创建路由守卫组件实现守卫逻辑
2. 创建 Fallback 组件用于渲染验证过程中的等待 ui
3. 在定义路由规则的组件中调用路由守卫组件对专题页面进行保护
4. 实现批量路由组件的保护功能

① 创建路由守卫组件实现守卫逻辑

```react
// src/shared/protected/index.js
import React,{useState, useEffect, useCallback} from "react";
import {Navigate} from "react-router-dom";

// guards 数组 用于存储验证函数 验证函数返回布尔值表示验证是否通过 验证函数必须是异步函数
// redirectPath 字符串 验证失败之后的跳转地址
// fallback jsx 验证过程中渲染的回退界面
export default function ProtectedRoute({guards, redirectPath, children, fallback}) {
	// valid 用于表示是否验证通过
	// status 用于表示验证状态
	const [{valid, status}, setState] = useState({valid: false, status: "idle"});
	// 验证函数
	const validator = useCallback(async () => {
		// 更新状态
		setState({valid: false, status: "processing"});
		// 验证中...
		const valid = (await Promise.all(guards.map((guard) => guard()))).every((item) => item);
		// 更新状态
		setState({valid, status: "completed"});
	}, [guards]);
	// 当验证函数发生变化以后重新验证
	useEffect(() => {
		validator();
	}, [validator]);
	// 如果正在验证 渲染回退 ui
	if (status === "processing") return fallback;
	// 如果验证完成
	if (status === "completed") {
		// 判断是否验证通过
		if (valid) {
			// 渲染子节点
			return children;
		} else {
			// 跳转
			return <Navigate to={redirectPath} replace />
		}
	}
	return null;
}
```

② 创建 Fallback 组件用于渲染验证过程中的等待 ui

```react
// src/shared/fallback/index.js
import React from "react";

export default function Fallback() {
	return <div>loading...</div>
}
```

③ 在定义路由规则的组件中调用路由守卫组件对专题页面进行保护

```react
// src/index.js
import Fallback from "./shared/fallback";
import ProtectedRoute from "./shared/protected";

// 模拟验证用户是否登录
async function isAuth() {
	// 模拟请求延时动作
	await new Promise((resolve) => setTimeout(resolve, 2000));
	// 返回验证结果
	return true;
}

const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			{
				path: "topic",
				element: (
					<ProtectedRoute guards={[isAuth, isAdmin]} redirectPath="/login" fallback={<Fallback />}>
					<TopicPage />
					</ProtectedRoute>
				)
			}
		]
	}
])
```
④ 实现批量路由组件的保护功能

**目标：对新闻页面路由组件和团队简介页面组件进行保护**

```react
// src/index.js
const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			{
				path: "",
				element: <ProtectedRoute guards={[isAuth, isAdmin]} redirectPath="/login" fallback={<Fallback />} />,
				children: [
					{
						path: "news",
						element: <NewsPage />
					},
					{
						path: "team/:name",
						element: <TeamPage />
					}
				]
			}
		]
	}
])
```

```react
// src/shared/protected/index.js
import {Outlet} from "react-router-dom";

export default function ProtectedRoute() {
	// 如果验证完成
	if (status === "completed") {
		return valid ? (
			children ? (
				children
			): (
				<Outlet />
			)
		) : (
			<Navigate to={redirectPath} replace />
		)
	}
}
```

## 9. 配置滚动恢复

**目标：掌握在 React Router V6 中配置滚动恢复的方式**

滚动恢复是指在页面发生切换行为时把滚动条恢复到页面顶部

需求：从首页跳转到专题页以测试滚动恢复

1. 展示未配置滚动恢复时存在的问题
2. 配置滚动恢复修正滚动问题
3. 通过 Link 组件的 preventScrollReset 选项阻止滚动恢复

① 展示未配置滚动恢复时存在的问题

```react
// src/pages/home/index.js
export default function HomePage() {
	return (
		<div>
			<div style={{height: 1500}}></div>
			<Link to="/topic">专题</Link>
		</div>
	)
}
```
```react
// src/pages/topic/index.js
import React from "react";

export default function Topic() {
	return <div style={{height: 1500}}>Topic</div>
}
```
② 配置滚动恢复修正滚动问题

```react
// src/shared/layout/index.js
import {ScrollRestoration} from "react-router-dom";

export default function Layout() {
	return <ScrollRestoration />;
}
```

③ 通过Link 组件的 preventScrollReset 选项阻止滚动恢复

```react
<Link to="/topic" preventScrollReset={true}>专题</Link>
```

## 10. 懒加载路由组件

**目标：掌握在 React Router V6 中实现路由懒加载的方式**

默认情况下应用中所有的组件都被打包到了同一个文件中 就是说应用初始加载时就加载了所有的组件 这样会导致初始加载应用时间长用户体验差

解决办法就是在打包应用时以页面之间为单位 把不同的页面之间打包到不同的文件中 初始加载时只加载用户访问的页面组件

① 通过 React 提供的 lazy 方法和 Suspense 组件实现路由组件懒加载
lazy 方法用于懒加载组件 Suspense 组件用于渲染加载过程中的等待状态

```react
// src/index.js
import {lazy, Suspense} from "react";

// 通过懒加载的方式导入组件
const HomePage = lazy(() => import("./pages/home"));

const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			{
				path: "",
				element: (
					<Suspense fallback={<Fallback />}>
						<HomePage />
					</Suspense>
				)
			}
		]
	}
])
```

② 创建 loadable 方法复用 Suspense 组件

```react
// src/shared/loadable/index.js
import React, {Suspense} from "react";
import Fallback from "../fallback";

export default function loadable(Component) {
	return function (props) {
		return (
			<Suspense fallback={<Fallback />}>
				<Component {...props} />
			</Suspense>
		)
	}
}
```

```react
// src/index.js
// 1. 多行选择 按住鼠标滚动拖动
// 2. 选择下一个单词 alt + shift + =>
// 3. 选择到行尾: ctrl + shift + =>
// 4. 选择下一个字符: shift + =>
const HomePage = loadable(lazy(() => import("./pages/home")));
const LoginPage = loadable(lazy(() => import("./pages/login")));
const NewsPage = loadable(lazy(() => import("./pages/news")));
const CompanyNewsPage = loadable(lazy(() => import("./pages/news/company")));
const IndustryNewsPage = loadable(lazy(() => import("./pages/news.industry")));
const TeamPage = loadable(lazy(() => import("./pages/team")));
const TopicPage = loadable(lazy(() => import("./pages/topic")));
const Fallback = loadable(lazy(() => import("./shared/fallback")));
```

##  11. 配置路由加载器

**目标：掌握路由配置项 loader 的使用方式**

1. 路由 loader 配置项概述
2. 在新闻页面路由规则中配置 loader 获取组件所需数据
3. 在新闻路由组件中获取 loader 配置中获取到的数据并渲染
4. 优化加载等待时间长的问题

① 路由 loader 配置项概述

loader 配置项允许开发者在渲染路由组件之前先获取路由组件所需数据 数据获取完成后在渲染路由组件

loader 配置项的值是一个异步函数 该异步函数用于获取路由组件所需数据 数据获取完成后要作为该函数的返回值

```react
{
	path: "team/:name",
	element: <TeamPage />,
	loader: async({params}) => {}
}
```

需求：创建团队简介路由组件的loader 函数

```bash
npm install axios@1.1.3;
```

```react
// src/pages/team/index.js
export async function teamLoader() {
	// 模拟阻塞
	await new Promise((resolve) => setTimeout(resolve, 3000));
	// 
}
```

② 在团队简介路由规则中配置 loader 选项

```react
// src/index.js
import {teamLoader} from "./pages/team";

const router = createBrowserRouter([
	{
		path: "team/:name",
		element: <TeamPage />,
		loader: teamLoader
	}
]);
```

③ 在团队简介组件中获取 loader 函数返回的组件所需要得状态并渲染

```react
// src/pages/team/index.js
import {useLoaderData} from "react-router-dom";

export default function TeamPage() {
	// 获取 loader 函数返回的状态
	const {todos} = useLoaderDate();
	// 渲染视图
	return (
		<ul>{todos.map((todo) => (
			<li key={todos.id}>{todo.title}</li>
		))}</ul>
	)
}
```

④ 捕获路由 loader 配置项中抛出的错误

```react
// src/pages/error/index.js
// 创建发生错误时渲染的组件
import React from "react";

export default function ErrorPage() {
	return <div>发生了错误</div>
}
```

```react
// src/index.js
import ErrorPage from "./pages/error";

const router = createBrowserRouter([
	{
		path: "team/:name",
		element: <TeamPage />, 
   		loader: teamLoader,
    	errorElement: <ErrorPage />,
	}
])
```
⑤ 优化加载等待时间长的问题 

```react
// src/pages/team/index.js
import {defer} from "react-router-dom";

async function loadTodos() {
	await new Promise((resolve) => setTimeout(resolve, 3000));
	const response = await axios.get("https://jsonplaceholder.typicode.com/todos")
	return response.data;
}

export async function teamLoader() {
	return defer({
		todosPromise: loadTodos()
	})
}
```
```react
import {Suspense} from "react";
import {Await} from "react-router-dom";
import Fallback from "../../shared/fallback";

export default function TeamPage() {
	const {todosPromise} = useLoaderData();
	return (
		<Suspense fallback={<Fallback />}>
			<Await resolve={todosPromise} errorElement={<div>未获取到待办事项列表</div>}>
			{(todos) => (
				<ul>
					{todos.map((todo) => (
						<li key={todo.id}>{todo.title}</li>
					))}
				</ul>
			)}
			</Await>
		</Suspense>
	)
}
```

##  12. 配置 404 组件

**目标：掌握配置404 页面组件的方式**

创建 PageNotFound 组件用于展示用于访问了一个不存在的路由路径
配置 PageNotFound 组件对应的路由规则

① 创建 NotFoundPage 组件用于展示用于访问了一个不存在的路由路径

```react
// src/pages/notFound/index.js
import React from "react";

export default function NotFoundPage() {
	return <div>页面未找到</div>
}
```

② 配置 PageNotFound 组件对应的路由规则

```react
// src/index.js
import NotFoundPage from "./pages/notFound";

const router = createBrowserRouter([
	{
		path: "/",
		errorElement: <NotFoundPage />
	}
])
```

##  13. 编程式导航

**目标：掌握在组件中使用编程式导航的方式**

```react
// src/pages/home/index.js
import React from "react";
import {useNavigate} from "react-router-dom";

export default function HomePage() {
	const navigate = useNavigate();
	return <button onClick={() => navigate("/topic")}>跳转到专题页面</button>
}
```

## 14. 配置索引路由

**目标：掌握索引路由的配置方式**

当没有匹配的子级路由时通过索引路由可以指定默认的渲染内容

```react
// src/index.js
const router = createBrowserRouter([
	{
		path: "/",
		element: <Layout />,
		children: [
			{
				path: "news",
				element: <NewsPage />,
				children: [
					{
						index: true,
						element: <Navigate to="/news/company" />
					},
					{
						path: "company",
						element: <CompanyNewsPage />
					},
					{
						path: "industry",
						element: <IndustryNewsPage />
					}
				]
			}
		]
	}
])
```