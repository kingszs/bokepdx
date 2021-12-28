---
title: uniapp 组件通讯🔚
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG3.png
tags:
  - uniapp
categories:
  - 技术笔记
  - uniapp
---

::: tip 介绍
简答介绍 uniapp 组件通讯<br>
uniapp 简单的教程
:::

<!-- more -->

### uni.$on()和uni.$emit()

- uniapp 和 vue 不同的是，vue 数据传递直接是单向的，通过 eventBus 来实现，uniapp 已经封装了全局的 api.
- vue 示例
- Vue.prototype.\$bus = new Vue();
- uniapp 示例

```js
uni.$emit("selectAccount", {
  accountInfo: JSON.parse(JSON.stringify(accountInfo)),
})
uni.$on("selectAccount", (data) => {
  console.log("接收的数据:" + data)
})
//注意：在页面关闭时在onUnload生命周期中卸载，uni.$off();
```

### globalData

```js
globalData: {
  data: ""
}

//获取：
getApp().globalData.data
//设置：
getApp().globalData.data = ""
```

### store

- [详情查看]()

### subNvue 页面向 vue 页面传递数据

```js
//两种获取子窗体不同方式
const subNVue = uni.getSubNVueById("map_widget")
const subNVue = uni.getCurrentSubNVue()

//发送
subNVue.postMessage({
  type: "message",
  title: "我是来自 subNVue 子窗体的消息",
  content: "Hello, map_widget",
})

//监听
subNVue.onMessage((res) => {
  const data = res.data
})
```

### 页面跳转传递数据

```js
let data = {};

uni.navigateTo({
	url: 'url?data' + data
})

//接收
onLoad(option) {
	console.log(option);
}
```

### nvue 向 vue 通讯

```js
//可以使用uni.$emit和uni.$on进行通讯

//通过应用生命周期在App.vue中进行监听
//nvue页面
	uni.postMessage({test: "数据",value:"数据"})
//app.vue页面
	onUniNViewMessage:function(e){
  	console.log(JSON.stringify(e.data))
  }
```

### vue 向 nvue 页面通讯

- 在 vue 里使用 plus.webview.postMessageToUniNView(data,nvueId) 发送消息，data 为 JSON 格式（键值对的值仅支持 String），nvueId 为 nvue 所在 webview 的 id

```js
//vue发送数据

<script>
    export default {
        methods: {
            test() {
                var pages = getCurrentPages();
                var page = pages[pages.length - 2];
                var currentWebview = page.$getAppWebview();
                plus.webview.postMessageToUniNView({
                    num: "123"
                }, currentWebview.id);
                uni.navigateBack()
            }
        }
    }
</script>
```

```js
//nvue接收数据

const globalEvent = weex.requireModule('globalEvent');
created() {
    globalEvent.addEventListener("plusMessage", e => {
        console.log(e.data);
        if (e.data.num) {
          //存在num时才赋值，在nvue里调用uni的API也会触发plusMessage事件，所以需要判断需要的数据是否存在
            this.num = e.data.num
        }
    });
}
```
