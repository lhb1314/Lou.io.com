---
title: Html面试题
date: 2023-04-13 20:37:12
tags:
top_img: https://img2.baidu.com/it/u=2305673033,3647467526&fm=253&fmt=auto&app=138&f=JPEG?w=731&h=500
cover: https://img2.baidu.com/it/u=2305673033,3647467526&fm=253&fmt=auto&app=138&f=JPEG?w=731&h=500
---

#  HTML 高级面试题

##  1. Html 语以化

① 什么是 Html语以化

h5 是一门标记语言，他的每一个标记都有特殊的含义。

```html
<!-- 用于定义标题 -->
<h1></h1>
<!-- 用于定义页面头部区域或 section 区域的页眉 -->
<header></header>
<!-- 用于定义网页导航链接区域 -->
<nav></nav>
<!-- 用于定义页面主体内容, 一个页面只能使用一次 -->
<main></main>
<!-- 用于定义一个页面中的一块自成一体的内容, 可以有自己的 header、footer、section 等 -->
<article></article>
<!-- 在 article 外, 主要用于定义页面侧边栏区域 -->
<!-- 在 article 内, 主要用于定义主要内容的附属内容 -->
<aside></aside>
<!-- 表示有语义化的 div, 用于标记页面中的各个部分 -->
<section></section>
<!-- 用于定义页面底部区域 --> 
<footer></footer>
<!-- 用于定义标题组 -->
<hgroup></hgroup>
<!-- 用于标记强调文本 -->
<strong></strong>
<!-- 用于标记一个段落 -->
<p></p>
<!-- 用于标记一个独立的流内容, 比如图像、图标、代码等等 -->
<figure>
  <img src="/media/cc0-images/elephant-660-480.jpg" alt="Elephant at sunset">
  <figcaption>An elephant at sunset</figcaption>
</figure>
<!-- 用于标记时间 -->
<time>2011-01-28</time>
```

② HTML 语义化有什么好处

1. 语义化的 h5 让开发者更容易理解，增加可阅读性。
2. 搜索时能快速定位到重要内容。
3. 在没有 css 情况下能够让页面呈现出清晰的结构。
4. 利用标签的特点优化体验。

##  2. 块级元素与行内元素

① 元素排列位置

每个块元素各占据一行。
行内元素在一排显示，如果有剩余的空间无法承载当前行内元素，会在新的一行显示。

② 元素包含内容

块级元素可以包含行内元素，宽度默认 100%。
行内元素不能包含块级元素，只能包含内容有关的。

③ 盒子模型

块级元素都可以设置。
行内元素设置 宽 高 margin上小无效，可以设置 line-height。


##  3. src 属性和 href 属性的区别

src 和 href 都是用来引用外部资源的属性。

href 超文本引用，建立当前元素和文档之间的连接，常用 link 和 a 标签。

src 把指定的资源引用到当前的文档中，常用 script， img，ifram 标签。

href 会建立一个关联指向资源，而 src 是把资源嵌入当前文档。

```html
<link href="cssfile.css" />
<a href="http://www.webpage.com"></a>
<script src="myscript.js"></script>
<img src="mypic.jpg" />
<video src=""></video>
<audio src=""></audio>
```

##  4. 图形标记的 title 属性和 alt 属性

alt 表示备用，图像无法显示浏览器渲染 alt 指定内容。

title 表示图像标题，鼠标移动到图像显示 title 属性的内容。

```html
<img src="" title="鼠标移入图像时展示的内容" alt="图像无法显示时展示的内容"/>
```

## 5. label 标签的作用

label 标签是为鼠标点击 label 标签中的文本时，浏览器自动把焦点转到 label 关联的表单上。

```html
<form>
  <label for="male">男</label>
  <input type="radio" name="sex" id="male">
  <label for="female">女</label>
  <input type="radio" name="sex" id="female">
</form>
```

##  6. Get 和 Post 的区别

① Get 在浏览器回退时是无害的，而 Post 会在次提交请求。
② Get 的 URL 地址能被存为书签， 而 Post 不行。
③ Get 请求会被浏览器缓存，而 post 不会。
④ Get 请求只能 url 编码，而 post 支持多种编码。
⑤ Get 的参数会被浏览器保存到历史记录，post 不会。
⑥ Get 参数在 url 传送有长度限制，post 没有。
⑦ Get 比 post 更不安全。
⑧ Get 参数通过 url 传递，post 参数放在请求体中。