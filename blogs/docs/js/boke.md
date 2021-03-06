---
title: 介绍一下怎么搭建简单的博客网站🔚
date: 2021-12-22
cover: https://pan.zealsay.com/mweb/blog/WechatIMG11.png
tags:
  - vue
  - 随笔
categories:
  - 技术笔记
  - 博客搭建
sticky: 1
---

::: tip 介绍
使用 vuepress_blog 搭建的第一篇博客<br>
简单的教程
:::

<!-- more -->

## 利用免费资源搭建个人博客项目

`服务器和域名都是使用vercel免费资源，框架则是采用了vuepress。`

## 博客搭建

首先我们先把在本地创建一个文件夹以存放项目文件

## 安装

```
npx @vuepress-reco/theme-cli init

# or

npm install @vuepress-reco/theme-cli -g
theme-cli init

# or

yarn  add @vuepress-reco/theme-cli
theme-cli init
```

**如果你网络不是很好的情况下，可以自己去拉如下的仓库**

```
#这是我目前在使用的主题

git clone https://gitee.com/GodLikeZeal/vuepress_blog.git

# cd 进入文件夹内

 #安装依赖
 yarn install  # or npm install

 # 运行项目
 yarn run dev # or npm run dev

```

打开浏览器 localhost:8080 就能访问了

## github

如果没有 github 账号，可以自行注册一个。（国内的网站链接 github 有时会报错，建议挂个梯子 🪜）

连接 github 仓库

首先我们创建一个 github 仓库(过程略)。

然后在本地初始化 git

```
#cd 进入你的vuepress文件夹内

git init

git add .

git commit -m 'init'
```

然后连接远程仓库。

```
git remote add origin 你的 github 仓库地址

# 现在github主分支是main，而gitee主分支是master，所以需要做修改

git branch -M main

git push -u origin main

```

**如果一直 push 不上去 github 仓库，建议开全局代理，然后重新 push 一下就可以了**

# 博客部署

我们利用的是 vercel 的免费资源，所以我们需要先注册个 [vercel](https://vercel.com/) 账号

登录之后[dashboard](https://vercel.com/dashboard)

点击**New Project**按钮导入刚刚创建的 github 仓库

导入之后全部选择默认配置，博客会自己构建，以后每次本地 push 之后，vercel 会自动构建

## 更换域名

如果你不想用他的域名的话，可以进入你创建的项目，进入`settings>>domains`添加自己的域名
