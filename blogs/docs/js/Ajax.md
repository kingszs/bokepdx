# Ajax

> 前言

&emsp;&emsp;在 Ajax 出现之前，网页想要和服务器通信，最常用的方式是使用 form 表单；用户提交表单后，浏览器就开始跳转，服务器接收表单并处理，然后将新的网页返回给浏览器；整个过程用户都只有等待，用户之前的操作状态会丢失，并且服务器返回的新网页常常和之前网页的大部分内容相同，浪费带宽；可见，使用表单来进行网页和服务器的交互，会做很多无谓的工作，浪费资源，用户体验还差。<br>
&emsp;&emsp;Ajax 是 Asynchronous JavaScript and XML（异步的 JavaScript 与 XML 技术）的缩写，并不是 JavaScript 的一部分，而是网页与服务器通信的一系列技术的总称。网页使用 Ajax 与服务器通信，可以规避上述 form 表单存在的问题，页面不会刷新，用户不用等待请求的返回，可以继续在我们的网页上“冲浪”。第一个大规模使用 Ajax 的网页应用是 Gmail，Gmail 的出现让大家意识到网页还能这么玩，网页也能做得像桌面应用一样，打破了大家对网页应用的认知，可以说 Ajax 为 web 技术注入了灵魂。

### 优势与劣势

- 优势
  - 无刷新更新数据
  - 异步与服务器进行通信
  - 减轻服务器和带宽的压力，Ajax 的工作原理相当于在用户和服务器之间加了一个中间层，使用户操作与服务器响应异步化
  - 提高 web 性能，在传统模式中，数据提交是通过表单（form）来实现的，而数据获取是靠全页面刷新来重新获取整夜内容。Ajax 模式只是通过 XMLHttpRequest 对象向服务器端提交希望提交的数据，即按需发送。
- 劣势
  - 不同版本的浏览器对 XMLHttpRequest 对象支持度不足
  - 前进、后退的功能被破坏
  - 搜索引擎的支持度不够

### IE6 及以下兼容

```js
if (window.XMLHttpRequest) {
  //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
  xmlhttp = new XMLHttpRequest()
} else {
  // IE6, IE5 浏览器执行代码
  xmlhttp = new ActiveXObject("Microsoft.XMLHTTP")
}
```

### 实现步骤

```js
1:创建XMLHttpRequest对象
	const xhr = new XMLHttpRequest();
2:初始化请求(method:get/post async:true/false)
	xhr.open('method', url, async);
3:绑定 xhr.readyState 改变时调用的回调
	xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if (xhr.status === 200) {
        console.log(xhr.responseText)
        console.log('请求成功')
      } else {
        console.log('请求错误')
      }
    }
  }
4:设置请求头（可选）
	xhr.setRequestHeader('Accept', '*/*')
5:发送请求
	xhr.send();
```

### 状态码

**readyState**

```js
	0：请求未初始化
	1：服务器已经建立连接
	2：请求已接收
	3：请求处理中
	4：请求已完成
```

**status**

```js
status
	100——客户必须继续发出请求
  101——客户要求服务器根据请求转换HTTP协议版本

  200——交易成功
  201——提示知道新文件的URL
  202——接受和处理、但处理未完成
  203——返回信息不确定或不完整
  204——请求收到，但返回信息为空
  205——服务器完成了请求，用户代理必须复位当前已经浏览过的文件
  206——服务器已经完成了部分用户的GET请求

  300——请求的资源可在多处得到
  301——删除请求数据
  302——在其他地址发现了请求数据
  303——建议客户访问其他URL或访问方式
  304——客户端已经执行了GET，但文件未变化
  305——请求的资源必须从服务器指定的地址得到
  306——前一版本HTTP中使用的代码，现行版本中不再使用
  307——申明请求的资源临时性删除

  400——错误请求，如语法错误
  401——请求授权失败
  402——保留有效ChargeTo头响应
  403——请求不允许
  404——没有发现文件、查询或URl
  405——用户在Request-Line字段定义的方法不允许
  406——根据用户发送的Accept拖，请求资源不可访问
  407——类似401，用户必须首先在代理服务器上得到授权
  408——客户端没有在用户指定的饿时间内完成请求
  409——对当前资源状态，请求不能完成
  410——服务器上不再有此资源且无进一步的参考地址
  411——服务器拒绝用户定义的Content-Length属性请求
  412——一个或多个请求头字段在当前请求中错误
  413——请求的资源大于服务器允许的大小
  414——请求的资源URL长于服务器允许的长度
  415——请求资源不支持请求项目格式
  416——请求中包含Range请求头字段，在当前请求资源范围内没有range指示值，请求也不包含If-Range请求头字段
  417——服务器不满足请求Expect头字段指定的期望值，如果是代理服务器，可能是下一级服务器不能满足请求

  500——服务器产生内部错误
  501——服务器不支持请求的函数
  502——服务器暂时不可用，有时是为了防止发生系统过载
  503——服务器过载或暂停维修
  504——关口过载，服务器使用另一个关口或服务来响应用户，等待时间设定值较长
  505——服务器不支持或拒绝支请求头中指定的HTTP版本

```

### 设置 HTTP 请求超时处理

- xhr.timeout 的值只能在调用 xhr.open 之后且在 xhr.send 之前设置

```js
var xhr = new XMLHttpRequest()
xhr.open("GET", "/api/hello")
xhr.timeout = 2000 // 超时时间，单位是毫秒
xhr.ontimeout = function(e) {
  // XMLHttpRequest 超时，在此做超时的处理
}
xhr.send(null)
```

### 发送表单数据

```js
var xhr = new XMLHttpRequest()
// 实例化一个 FormData 对象
var formData = new FormData()
// 向 FormData 添加数据
formData.append("username", "whale")
formData.append("age", "18")
xhr.open("POST", "/api/form")
// 发送表单数据
xhr.send(formData)
```

### 上传文件

```js
;<input type="file" name="uploadFile" id="upload-file" />

var formData = new FormData()

formData.append("uploadFile", this.file[0])
xhr.send(formData)
```
