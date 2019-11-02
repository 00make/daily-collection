# 安装
---
Node.js 安装包及源码下载地址为：https://nodejs.org/en/download/

安装成功标准：cmd：node -v可显示版本号&node已加入path环境

> 安装新版node时有个附加工具会给你装一堆additional环境，简单好用



# 创建第一个应用
---
## Node.js 应用由三部分组成：

    引入 required 模块：我们可以使用 require 指令来载入 Node.js 模块。

    创建服务器：服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。

    接收请求与响应请求 服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。

## 步骤一、引入 required 模块

我们使用 require 指令来载入 http 模块，并将实例化的 HTTP 赋值给变量 http，实例如下:

```javascript
  //请求（require）Node.js 自带的 http 模块，并且把它赋值给 http 变量。
  var http = require("http");
  
```
## 步骤二、创建服务器

接下来我们使用 http.createServer() 方法创建服务器，并使用 listen 方法绑定 8888 端口。 函数通过 request, response 参数来接收和响应数据。

```javascript
    // 调用 http 模块提供的函数： createServer 。这个函数会返回 一个对象，这个对象有一个叫做 listen 的方法。
http.createServer(function (request, response) {

    // 发送 HTTP 头部 状态值 200 : OK
    // 内容类型: text/plain
    response.writeHead(200, {'Content-Type': 'text/plain'});

    // 发送响应数据 "Hello World"
    response.end('Hello World\n');
    
    //listen有一个数值参数， 指定这个 HTTP 服务器监听的端口号。
}).listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');
```



将步骤一步骤二代码打包至node.js后，使用 node 命令执行以上的代码：

```javascript
node node.js
Server running at http://127.0.0.1:8888/
```

接下来，打开浏览器访问 http://127.0.0.1:8888/   ,会看到一个写着 "Hello World"的网页，第一个应用创建成功。

