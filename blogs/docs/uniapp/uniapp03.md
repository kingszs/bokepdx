---
title: uniapp å¨å±åéð
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG2.png
tags:
  - uniapp
categories:
  - ææ¯ç¬è®°
  - uniapp
---

::: tip ä»ç»
ç®ç­ä»ç» uniapp å¨å±åé<br>
uniapp ç®åçæç¨
:::

<!-- more -->

### ä»ç»

é¡¹ç®å¼åä¸­ï¼ä¼ä½¿ç¨ä¸äºå¨å±çåéæèæ¹æ³ï¼è¿æ¶åæä»¬éè¦å»å°è£èµ·æ¥ï¼æ¾å¨ä¸ä¸ªå¬å±çå°æ¹ï¼æ¹ä¾¿ä½¿ç¨ãä¸é¢ä»ç»ä¸ç§å¸¸ç¨çæ¹æ³ã

### æè½½ Vue.prototype

å°ä¸äºå¸¸ç¨åéåæ¹æ³æè½½å¨ vue çååä¸ï¼è¿æ ·æ¯ä¸ª vue çå¯¹è±¡é½ä¼ç»§æ¿ä¸æ¥ï¼å¯ä»¥ç´æ¥éè¿ this å»è®¿é®ã

```js
//æè½½

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
//ä½¿ç¨

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

å¨ uniapp ä¸­,globalData ç¨äºå®ä¹å¨å±åéï¼ä½¿ç¨èµ·æ¥ä¹éå¸¸æ¹ä¾¿

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
    /*æ¯ä¸ªé¡µé¢å¬å±css */
</style>
```

```js
//èµå¼
getApp().globalData.text = "test"

//åå¼
getApp().globalData.text
```

### Vuex

Vuex æ¯ä¸ä¸ªä¸ä¸º Vue.js åºç¨ç¨åºå¼åçç¶æç®¡çæ¨¡å¼ãå®éç¨éä¸­å¼å­å¨ç®¡çåºç¨çææç»ä»¶çç¶æï¼å¹¶ä»¥ç¸åºçè§åä¿è¯ç¶æä»¥ä¸ç§å¯é¢æµçæ¹å¼åçååã
