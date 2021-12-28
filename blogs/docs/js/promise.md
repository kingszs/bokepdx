---
title: promise🔚
date: 2021-12-28
cover: https://pan.zealsay.com/mweb/blog/WechatIMG8.png
tags:
  - js
  - promise
categories:
  - 技术笔记
  - js相关技术
---

::: tip 介绍
promise 相关介绍<br>
简单的教程
:::

<!-- more -->

# promise

### promise 的三种状态

- promise 是一种异步的操作，它有三种状态,Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败)，实际变化只有下面两种状态,一旦改变就不可以修改。
- Pending -> Resolved
- Pending -> Rejected

**例子**

```js
new Promise(function(resolve, reject){
    const a = 1;
    if(a === 1){
        resolve(a)
    }else{
        reject('error)
    }
}).then(function(value){
    console.log(value)
}).catch(function(error){
    console.log(error)
})
```

### finally

- finally 方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。finally 方法的回调函数不接受任何参数。

```js
let profiy = new Promise((resolve, reject) => {
  if (true) {
    resolve("哈哈哈")
  }
})
  .then((res) => {
    console.log("res:" + res)
  })
  .catch((error) => {
    console.log("errpr:" + error)
  })
  .finally(() => {
    console.log("呵呵呵")
  })
// 哈哈哈  呵呵呵
```

promise.all()

- Promsie.all() 方法用于将多个 Promise 实例包装成一个新的 Promise 实例。

```js
let p = Promise.all([p1, p2, p3])
```

- p 的状态是由 p1,p2,p3 共同决定,有两种情况
  - 当 p1,p2,p3 的状态都是成功时，p 的状态才是成功的,此时 p1,p2,p3 的返回值会组成一个数组,返回给 p
  - 当 p1,p2,p3 的状态有一个失败时，p 的状态也是失败，如果 p1,p2,p3 有自己的 catch 就会执行自己的，没有则执行 p 的 catch 方法。

```js
//都成功情况
let p1 = new Promise((resolve, reject) => {
  resolve("p1")
})

let p2 = new Promise((resolve, reject) => {
  resolve("p2")
})

Promise.all([p1, p2])
  .then((res) => {
    console.log(res)
  })
  .catch((error) => {
    console.log("error:" + error)
  })

// ['p1', 'p2']
```

```js
//失败情况
let p1 = new Promise((resolve, reject) => {
  resolve("p1")
})

let p2 = new Promise((resolve, reject) => {
  // resolve('p2');
  throw new Error("报错了")
}).catch((error) => {
  console.log("p2 error:" + error)
})

Promise.all([p1, p2])
  .then((res) => {
    console.log(res)
  })
  .catch((error) => {
    console.log(error)
  })
//Error: 报错了	//Promise.all()有自己的catch,会执行Promise.all()的，如果没有则执行自己的catch
```

### promise.race()

- Promise.race() 方法也是将多个 Promise 实例，包装成一个新的 Promise 实例.
- 如果 p1,p2,p3 中有一个实例先改变，那么最先改变的状态的实例返回值就会传递给 p,谁先执行完就会返回谁的值。

```js
const p = Promise.race([p1, p2, p3])

//实例
let p1 = new Promise((resolve, reject) => {
  resolve("p1")
})

let p2 = new Promise((resolve, reject) => {
  resolve("p2")
}).catch((error) => {
  console.log("p2 error:" + error)
})

Promise.race([p1, p2]).then((res) => {
  console.log(res)
})

//p1		p1先执行，将数据返回到方法的回调函数中去。
```

### promise 封装 ajax

```js
const getJSON = function(url) {
  const promise = new Promise(function(resolve, reject) {
    const handler = function() {
      if (this.readyState !== 4) {
        return
      }
      if (this.status === 200) {
        resolve(this.response)
      } else {
        reject(new Error(this.statusText))
      }
    }
    const client = new XMLHttpRequest()
    client.open("GET", url)
    client.onreadystatechange = handler
    client.responseType = "json"
    client.setRequestHeader("Accept", "application/json")
    client.send()
  })
  return promise
}
```
