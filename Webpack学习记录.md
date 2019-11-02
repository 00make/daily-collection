# 介绍
---
Webpack 是一个前端资源加载/打包工具，根据模块的关系进行静态分析，然后将这些模块按照的规则生成对应的静态资源。
在实例中，可以将多种静态资源 js、css、less 转换成一个静态文件，减少了页面的请求。

# 安装
---
在安装 Webpack 前，本地环境需要支持 node.js

由于 npm 安装速度慢，本教程使用了淘宝的镜像及其命令 cnpm，安装使用参照：node.js学习记录-NPM使用介绍-使用淘宝 NPM 镜像
```javascript
npm install webpack -g   //使用 npm 安装 webpack
npm install webpack-cli -g 
cnpm install webpack -g  //使用 cnpm 安装 webpack
cnpm install webpack-cli -g
```

# 使用webpack打包
---
假设在一个app 目录下，存在runoob1.js，runoob1.js和index.html 三个文件

runoob1.js 文件代码如下：
```javascript
document.write("It works.");
```

runoob2.js 文件代码如下：
```javascript
module.exports = "It works from runoob2.js.";
```

index.html 文件代码如下
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <script type="text/javascript" src="bundle.js" charset="utf-8"></script>
    </body>
</html>
```

进行打包
```javascript
webpack runoob1.js bundle.js  //其实这一步我运行时无法正确生成，报Error: Cannot find module 'webpack-cli'，我都装了一下
```
执行以上命令会编译 runoob1.js 文件并生成bundle.js 文件
webpack 根据模块的依赖关系进行静态分析，这些文件(模块)会被包含到 bundle.js 文件中。
Webpack 会给每个模块分配一个唯一的 id 并通过这个 id 索引和访问模块。
在页面启动时，会先执行 runoob1.js 中的代码，其它模块会在运行 require 的时候再执行。

    Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。
    
参考菜鸟教程webpack教程 https://www.runoob.com/w3cnote/webpack-tutorial.html
