# 安装
 ---
 
需要有nodejs初始环境 
在cmd内，运行如下
安装express（选择安装）cnpm install -g express
安装webpack           cnpm install -g webpack
安装vue               cnpm install vue
安装 vue-cli          cnpm install -g vue-cli


# 开始项目初始化。
---

在cmd里用cd命令跳转到指定目录，运行项目初始化命令：
```javascript
vue init webpack [vue-projectname]    //这个过程中会下载官方模板&进行项目初始化
                                      //vue-projectname文件夹会自动生成在你跳转到的目录中
```


cd到我们的项目文件夹d:\Vue\vue-projectname中，运行命令
```javascript
cnpm install
```


测试项目是否安装成功。
```javascript
cnpm run dev
```


# 第一个实例
---
```html
 <!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <p>{{ message }}</p>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }
})
</script>
</body>
</html>
```
