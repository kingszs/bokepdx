---
title: uniapp 全局变量🔚
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG2.png
tags:
  - uniapp
categories:
  - 技术笔记
  - uniapp
---

::: tip 介绍
简答介绍 uniapp 全局变量<br>
uniapp 简单的教程
:::

<!-- more -->

### 介绍

项目开发中，会使用一些全局的变量或者方法，这时候我们需要去封装起来，放在一个公共的地方，方便使用。下面介绍三种常用的方法。

### 挂载 Vue.prototype

将一些常用变量和方法挂载在 vue 的原型上，这样每个 vue 的对象都会继承下来，可以直接通过 this 去访问。

```js
//挂载

Vue.prototype.websiteUrl = "www.along.ink"
Vue.prototype.now =
  Date.now ||
  function() {
    return new Date().getTime()
  }
Vue.prototype.isArray =
  Array.isArray ||
  function(obj) {
    return obj instanceof Array
  }
```

```js
//使用

<script>
    export default {
        data() {
            return {};
        },
        onLoad(){
            console.log('now:' + this.now());
        },
        methods: {
        }
    }
</script>
```

### globalData

在 uniapp 中,globalData 用于定义全局变量，使用起来也非常方便

```js
<script>
    export default {
        globalData: {
            text: 'text'
        },
        onLaunch: function() {
            console.log('App Launch')
        },
        onShow: function() {
            console.log('App Show')
        },
        onHide: function() {
            console.log('App Hide')
        }
    }
</script>

<style>
    /*每个页面公共css */
</style>
```

```js
//赋值
getApp().globalData.text = "test"

//取值
getApp().globalData.text
```

### Vuex

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
