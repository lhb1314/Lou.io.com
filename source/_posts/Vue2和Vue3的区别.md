---
title: Vue2 和 Vue3 的区别
date: 2023-04-04 17:10:20
tags: Lou
comments: true
top_img: https://img0.baidu.com/it/u=3186304939,1761512753&fm=253&fmt=auto&app=138&f=JPG?w=500&h=281
cover: https://img0.baidu.com/it/u=3186304939,1761512753&fm=253&fmt=auto&app=138&f=JPG?w=500&h=281
---

# Vue2 和 Vue3 的区别
目标：了解 Vue2 和 Vue3 的区别

## Composition API
这是 vue2 和 vue3 之间最大的区别
vue2 使用选项类型 API（Options API）相比之下
vue3 使用合成型 API （Composition API）

## vue2 和 vue3 双向绑定原理发生了改变
vue2 的双向绑定是利用 ES5 的一个 API Object.definePropert() 对数据进行结合 发布定阅模式的方式来实现的。
vue3 中使用了 es6 的 Proxy API 对数据代理

## Vue3 支持碎片（Fragments）
就是说在组件可以拥有多个根节点

## 建立数据
Vue2 这里把数据放入 data 属性中
Vue3 我们就需要使用一个新的 setup() 方法 方法在组件初始化构造的时候触发

## 生命周期钩子不同 Lifecyle Hooks

| Vue2 | Vue3 |
| :--: | :------: |
| beforeCreate | setup() |
| created | setup() |
| beforeMount | onBeforeMount |
| mounted | onMounted |
| beforeUpdate | onBeforeUpdate |
| updated | onUpdated |
| beforeDestroy | onBeforeUnmount |
| destroyed | onUnmounted |
| activated | onActivated |
| deactivated | onDeactivated |

## 父子传参不同
vue3 新增了 Teleprot 瞬移组件

