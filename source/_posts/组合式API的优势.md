---
title: 组合式API的优势
date: 2022-06-24
tags:
top_img: https://img0.baidu.com/it/u=478577661,3334797226&fm=253&fmt=auto&app=138&f=JPEG?w=499&h=320
cover: https://img0.baidu.com/it/u=478577661,3334797226&fm=253&fmt=auto&app=138&f=JPEG?w=499&h=320
---
 
## 组合式 API 的优势
目标：掌握组合式 API 相比较选择 API 他的优势是什么

在选项式API中，它将数据和逻辑进行了分离，所有不相关的数据被放置在了一起，所以不相关的逻辑被放置在了一起，随着应用规模的增加，项目将会变得越来越难以维护。

```tsx
export default {
  data: {
    // A...
    // B...
  	// C...
  },
  methods: {
    // A...
    // B...
  	// C...
  },
  computed: {
    // A...
    // B...
  	// C...
  },
  watch: {
    // A...
    // B...
  	// C...
  },
  directives: {
    // A...
    // B...
  	// C...
  }
}
```
{% asset_img 1.gif This is an example image %}

在组合式 API 中 他把同一个功能的逻辑和数据发到一起 使同一个的功能和代码更加居合

```tsx
export default {
  setup () {
    // 属性
    // 方法
    // 计算属性
    // 数据监听
    // ......
  }
}

```
```tsx
export default {
  setup () {
    // A...
    // B...
    // C...
  }
}

```
{% asset_img 2.gif This is an example image %}
同一个功能的代码可以被抽取到单独的文件中 使应用代码更加维护

```tsx
export default {
	setup(){
		useFunc_1();
		useFunc_2();
	}
}
function useFunc_1() {}
function useFunc_2() {}

```
{% asset_img 3.gif This is an example image %}

## 组合式 API 入口

目标：掌握 setup 函数的基本使用

- 讲解 setup 函数的执行时机以及 this
- 讲解 setup 函数的返回值的作用以及注意事
setup 函数是一个新的组件选择

```tsx
export default {
  setup () {}
}

```

setup 函数在任何生命周期函数之前执行，且函数内部 this 为 undefined，它不绑定组件实例对象

```tsx
export default {
  setup() {
    console.log(this) // 1. undefined
  },
  beforeCreate() {
    console.log("before create") // 2. before create
  },
}

```

setup 函数的返回值必须是对象，对象中的属性会被添加到组件实例对象中，所以它们可以在其他选项和模板中使用

```tsx
export default {
  setup() {
    let name = "张三"
    let age = 20
    return { name, age }
  },
  beforeCreate() {
    console.log(this.name);
  },
}

```
注意：在 setup 方法中声明的变量虽然可以在模板中显示，但它不是响应式数据，就是说当数据发生变化后视图不会更新。

```tsx
 export default {
    setup() {
      let name = "张三"
      let age = 20
      const onClickHandler = () => {
        name = "李四"
        age = 30
      }
      return { name, age, onClickHandler }
    }
  }

```
```tsx
  <template>
    {{ name }} | {{ age }} 
  	<button @click="onClickHandler">button</button>
  </template>

```