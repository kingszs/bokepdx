---
title: uniapp 页面样式哦与布局🔚
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG1.png
tags:
  - uniapp
categories:
  - 技术笔记
  - uniapp
---

::: tip 介绍
简答介绍 uniapp 页面样式哦与布局<br>
简单的教程
:::

<!-- more -->

### 单位

&emsp;uniapp 支持通用的 css 单位包括 px 与 rpx。不推荐使用 upx。

### 样式导入

```html
//使用@import语句可以导入外联样式表
<style>
  @import "../../common/uni.css";

  .uni-card {
    box-shadow: none;
  }
</style>
```

### 设置背景

```css
//在uniapp不能使用*选择器，page相当于body
// 设置页面背景颜色
page {
  background-color: #ccc;
}
```

### 全局样式与局部样式

<p>&emsp;定义在 App.vue 中的样式为全局样式，作用于每一个页面。在 pages 目录下 的 vue 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 App.vue 中相同的选择器。
在 app.vue 通过@import 导入的样式同样作用于每个页面</p>

#### css 变量

快速书写 css 变量的方法是：在 css 中敲 hei，在候选助手中即可看到 3 个 css 变量。（HBuilderX 1.9.6 以上支持）

示例 1 - 普通页面使用 css 变量：

```js
<template>
    <!-- HBuilderX 2.6.3+ 新增 page-meta, 详情：https://uniapp.dcloud.io/component/page-meta -->
    <page-meta>
        <navigation-bar />
    </page-meta>
    <view>
        <view class="status_bar">
            <!-- 这里是状态栏 -->
        </view>
        <view> 状态栏下的文字 </view>
    </view>
</template>
<style>
    .status_bar {
        height: var(--status-bar-height);
        width: 100%;
    }
</style>
```

```js
<template>
    <view>
        <view class="toTop">
            <!-- 这里可以放一个向上箭头，它距离底部tabbar上浮10px-->
        </view>
    </view>
</template>
<style>
    .toTop {
        bottom: calc(var(--window-bottom) + 10px)
    }
</style>
```

#### 示例 2 - nvue 页面获取状态栏高度

```js
<template>
    <view class="content">
        <view :style="{ height: iStatusBarHeight + 'px'}"></view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                iStatusBarHeight:0
            }
        },
        onLoad() {
            this.iStatusBarHeight = uni.getSystemInfoSync().statusBarHeight
        }
    }
</script>
```

### <template/>与<block/>

uniapp 支持在 templat 中嵌套 block 用来进行列表渲染和条件渲染。
