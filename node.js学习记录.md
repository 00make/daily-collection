# node.js学习记录
---

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




# NPM 使用介绍
---
NPM是随同NodeJS一起安装的包管理工具，
允许用户从NPM服务器（上传，下载，安装）（本地或别人）编写的（第三方包或命令行程序）到（本地或供别人）使用。

## 安装测试
```javascript
npm -v          //测试是否成功安装
npm install npm -g        //windows升级npm可使用命令 
npm install -g cnpm --registry=https://registry.npm.taobao.org    //通过（淘宝）镜像升级npm可使用命令
```
    

## 使用淘宝 NPM 镜像

使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:
```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

这样就可以使用 cnpm 命令来安装模块了：
```javascript
cnpm install [name]
```

## 使用 npm 安装各种模块

以下实例，我们使用 npm 命令安装常用的 Node.js web框架模块 express:
```javascript
npm install express      //本地安装
npm install express -g   //全局安装
```

安装好之后，express 包就放在了工程目录下的 node_modules 目录中，因此在代码中只需要通过 require('express') 的方式就好，无需指定第三方包路径。
```javascript
var express = require('express');
```

## 常用命令

```javascript
npm list              //查看所有本地安装的模块
npm list -g           //查看所有全局安装的模块
npm uninstall express //卸载模块
npm update express    //更新模块
npm help              //查看所有命令

```
