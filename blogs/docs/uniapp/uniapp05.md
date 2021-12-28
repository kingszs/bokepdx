---
title: uniapp 原生视频控件🔚
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG5.png
tags:
  - uniapp
categories:
  - 技术笔记
  - uniapp
---

::: tip 介绍
简答介绍 uniapp 原生视频控件<br>
uniapp 简单的教程
:::

<!-- more -->

### 初始化视频

```js
this.player = player = plus.video.createVideoPlayer("videoplayer", {
  src: "http://cdn.zsdx.cn/wei/images/hire/home/home_video.mp4",
  top: "30px",
  left: "0px",
  width: "auto",
  height: "250px",
  position: "static",
})
plus.webview.currentWebview().append(player)
```

### 播放视频

```js
this.player.play()
```

### 监听视频播放

```js
this.player.addEventListener('play', (e)=> {
	uni.showToast({
    title: '开始播放',
    icon: 'none',
    dura	tion: 3000
	});
}, false)
```

### 监听播放速度

```js
this.player.addEventListener(
  "timeupdate",
  (e) => {
    self.timeupdate = e.detail.currentTime
  },
  false
)
```

### 暂停播放

```js
this.player.pause()
```

### 停止播放

```js
this.player.stop()
```

### 监听播放结束

```js
this.player.addEventListener(
  "ended",
  function(e) {
    uni.showToast({
      title: "播放结束",
      icon: "none",
      duration: 3000,
    })
  },
  false
)
```

### 设置全屏/退出全屏

```js
//0（正常竖向）, 90（屏幕逆时针90度）, -90（屏幕顺时针90度）
this.player.requestFullScreen(-90)
```

### 显示播放控件

```js
this.player.show()
```

### 关闭播放控件

```js
this.player.close()
```

### 设置播放倍速

```js
data () {
	return {
  		index: 0
  }
}

let option = ['0.5', '0.8', '1.0', '1.25', '1.5'];
uni.showToast({
    title: `${option[this.index]}倍速`,
    icon: 'none',
    duration: 3000
});

this.player.playbackRate(option[this.index]);
this.index ++;

if (this.index == 5) {
		this.index = 0;
}
```
