---
title: 学习Vue
date: 2019-11-06 23:29:12
tags: Vue
categories: 学习
comments: true
---



学习Vue的一些笔记

<!--more-->

## 基础：

1.前后端交互

前段工作：SPA   页面导航功能（Vue Router）、组件之间公共信息保存（Vuex）、服务器数据资源请求（axios）、权限和安全。

（1）Vue Router

路由管理器，构建单页面应用

（2）Vuex

状态管理器。集中式存储管理应用的所有组件状态



## 问题记录：

### 1.在vue项目中，执行 npm run dev 时提示{ parser: "babylon" } is deprecated; we now treat it as { parser: "babel" }
问题原因：是prettier版本导致的，重装prettier：npm install prettier@~1.12.0 -D或者cnpm install prettier@~1.12.0 --save-dev,然后重新npm run dev
解决办法：
找到modules包里面的：node_modules\vue-loader\lib\template-compiler\index.js
将{ parser: "babylon" } 换成  { parser: "babel" } 即可

### 2.修改了App.vue后，提示“Component template should contain exactly one root element. If you are using v-if on multiple elements, use v-else-if to chain them instead.”
问题原因：**vue模板只能有一个根对象**
解决方法：用一个div来或是别的标签来包裹全部的元素
```
<template>
    <div>
        <el-button type="primary">button_1</el-button>
        <div>div_1</div>
        <el-input type="text" placeholder="测试一下"></el-input>
        <h1>{{test1}}</h1>
    </div>
</template>
```