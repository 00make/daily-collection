# vue组件使用分三步：
```javascript
1. 引用组件 import facePop from './components/facePop'
2. 注册组件 components = { facePop }
3. 使用组件 <facePop></facePop>
```
# 新建一个components文件夹存放组件

- src/components/facePop.vue
    
```javascript
<template>
    <div>
        <h2>我是一个facePop组件</h2>
    </div>
</template>
```


- src/index.vue

```javascript
<template>
  <div>
    <facePop></facePop>                   <!--3、在模板中使用kebab-case 两种都可以-->
    <face-pop></face-pop>                 <!--3、在模板中使用PascalCase-->
  </div>
</template>
<script>
  import facePop from './components/facePop';     //1、引入组件 import后的名字一般与组件名称相同，也可不一样
  export default{
    data(){},
    components:{
     facePop       //2、注册组件 一般直接取一个名字  即：facePop：facePop
    }
  }
</script>
```

# [案例]一个页面使用多个组件
- src/app.vue
```javascript
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
    <Hello/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Hello from './components/Hello';

export default {
  name: 'App',
    data () {
        return {msg: 'layout'}
    },
  components: {
    HelloWorld,
    Hello
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```
# 组件名大小写

## 定义组件名的方式有两种：
- 使用 kebab-case
    Vue.component('my-component-name', { /* ... / })
    当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 <my-component-name>。
- 使用 PascalCase
    Vue.component('MyComponentName', { / ... */ })
    当使用 PascalCase (首字母大写命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 <my-component-name> 和 <MyComponentName> 都是可接受的。注意，尽管如此，直接在 DOM (即非字符串的模板) 中使用时只有 kebab-case 是有效的。
    我们使用字符串模板，所以这个限制就不存在了



# 组件之间传值
 【1】父组件给子组件传值：

    1）父组件调用子组件的时候绑定动态属性
    2）子组件里通过props（props可以接收一个数组或对象，接收对象时可对数据进行校验如：{title:String}，可以校验组件传过来的是否为String）接收父组件传过来的数据
    总结：父组件传值给子组件（父组件绑定数据如:list="list"，子组件通过props获取）
    子组件的props选项能够接收来自父组件数据。没错，仅仅只能接收，props是单向绑定的，即只能父组件向子组件传递，不能反向。

## 传递方式分为两种：
- 静态传递：
    子组件通过props选项来声明一个自定义的属性，然后父组件就可以在嵌套标签的时候，通过这个属性往子组件传递数据了

<v-facePop showFaceDia=“这是文字”></v-facePop> // 此处showFaceDia不加冒号
子组件：
```javascript
props:{
  showFaceDia: String
}
```

- 动态传递：

父组件：
```javascript
data: 
{ 
    showFaceDia: false 
}
<v-facePop :showFaceDia=“showFaceDia”></v-facePop>
```
子组件：
```javascript
props:{
  showFaceDia: Boolean
}
```
# 子组件向父组件传值 （vue写法）

子组件中：
```javascript
this.showFaceDia = false  
this.$emit('showFaceDia',this.showFaceDia)  //执行showFaceDia函数并把要改变的值作为参数带过去
```
父组件：
```javascript
methods:{
showFaceDia(msg){
    this.showFaceDia = msg
  }
}
```
不要忘记在DOM中引用：
<test :title="title" @showFaceDia="showFaceDia"></test>//注意showFaceDia后不能加括号

# 子组件向父组件传值 （wepy写法）

比如父组件中showFaceDia 默认为true
子组件中：
```javascript
this.showFaceDia = false  
this.$emit('showFaceDia',this.showFaceDia)  //执行showFaceDia函数并把要改变的值作为参数带过去
```
父组件：
```javascript
events = {
            showFaceDia(msg){
                this.showFaceDia = msg
            }
        }
```
# 父组件调用子组件的方法：
    ref用在子组件上，指向的是组件实例，可以理解为对子组件的索引，通过$ref可以获取到在子组件里定义的属性和方法

//父组件
```javascript
<v-test :title="title" ref="aa"></v-test> //通过ref为子组件赋予ID引用
<div @click="getChild()"></div>
getChild(){
  this.$refs.aa.childFun()   // 此处使用
}
```
# 子组件调用父组件的方法：

- （1）直接在子组件中通过this.$parent.event来调用父组件的方法
- （2）在子组件里用$emit向父组件触发一个事件，父组件监听这个事件就行了实例:


子组件：
```javascript
methods: {
        getParent () {
            this.$emit('togglePop')  //此处直接写父组件的事件名称
        }
    }
 ```
父组件：
```javascript
DOM中：<test :title="title" @togglePop="togglePop"></test>
togglePop(){
            console.log('ddddddd')
        },
 ```

wepy中的写法：https://tencent.github.io/wepy/document.html#/?id=%E7%BB%84%E4%BB%B6%E9%80%9A%E4%BF%A1%E4%B8%8E%E4%BA%A4%E4%BA%92

父组件：
```javascript
DOM中：
<facePop @parentFn.user="togglePop"></facePop>
子组件DOM和方法：
<view @tap="getParent"></view>
methods: {
        getParent () {
            this.$emit('parentFn')  
        }
    }
```
通过父组件向子组件传不同的值作为标识，可以有针对性的对各父组件进行个性化的操作。

父组件1:
```javascript
data(){
  proDetail: 'proDetail'
}
<test :proDetail='proDetail'></test>
```
子组件：
```javascript
props:{
  proDetail: String
}
if(this.proDetail === 'proDetail'){ ... } //此时针对父组件1的一系列操作
```
