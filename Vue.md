# Vue面经

## Vue优缺点

### 优点

#### 渐进式

通俗点讲就是，你想用啥就学啥

一开始不需要你完全掌握它的全部功能特性，可以后续逐步增加功能。没有多做职责之外的事情

#### 组件化

##### 为什么要做组件化？

传统开发方式`效率低`以及`维护成本高`的主要原因在于很多时候是将一个系统做成了整块应用，而且往往随着业务的增长或者变更，系统的复杂度会呈现指数级的增长，经常出现的情况就是一个小小的改动或者一个小功能的增加可能会引起整体逻辑的修改，造成牵一发而动全身

##### 组件化的意义：

不相互依赖，可以相互交互，任意组合，高度解耦，自由拆卸，自由组装，重复利用，分层独立化。

##### 组件的使用场景

在系统业务复杂的情况下将其拆分成数个组件，提升开发效率，降低维护成本

#### 轻量级



虚拟dom

响应式

单页面路由

数据与视图分开



### 缺点

单页面不利于seo

不支持IE8以下版本

首屏加载时间长





































































# Vue2.x

## vue router

### 动态路由

### 编程式导航







# Vue3

## Vite

`vite`是尤雨溪团队开发的新一代的前端构建工具，意图取代**webpack**

### `vite`优点：

- 无需打包，快速的冷服务器启动
- 即时热模块更换（HMR，热更新）
- 真正的按需编译

### 与``webpack`对比

#### `webpack`

是一开始是`入口文件`，然后`分析路由`，然后`模块`，最后进行`打包`，然后告诉你，服务器准备好了（默认8080）

#### ![bundler.37740380.png](assets/4dcb2c8157004850ad319f478cea528btplv-k3u1fbpfcp-watermark.awebp)`vite`

一开始是先告诉你服务器准备完成，然后等你发送HTTP请求，然后是入口文件，`Dynamic import`（动态导入）`code split point`（代码分割）

![esm.3070012d.png](assets/dedecd49c0344bf5b11f3fa3e4910787tplv-k3u1fbpfcp-watermark.awebp)



### 使用

> //要构建一个 Vite + Vue 项目，运行，使用 NPM:npm init @vitejs/app 项目名
> //使用 Yarn:
> yarn create @vitejs/app 项目名

> 你会觉得非常快速的创建了项目，然而它并没有给你下载依赖，你还有进入文件然后
> npm install (or yarn)



#### 打开方式

不是 `serve` 变成了`dev`

![1636687125(1).png](assets/37464be282ed4d20bac0a27a680c0a52tplv-k3u1fbpfcp-watermark.awebp)



## vue3 变化

### main.js

![1636688554(1).jpg](assets/e91e06642dc64e3fa93bf57aad29359btplv-k3u1fbpfcp-watermark.awebp)

![1636688564(1).jpg](assets/9b0acecab2ed4c05a5ad458eb1b31826tplv-k3u1fbpfcp-watermark.awebp)引入的不是vue构造函数，而是`createApp`工厂函数然而，创建实例对象其实就相当于vue2中的`vm`，`mount（'#app'）`就相当于`$mount('#app')`，并且vue2的写法在vue3不能兼容



现在我们进入App组件，你会发现什么不一样的地方，他`没有了根标签`，在vue2的时候，我们都是在div根标签里面写东西，所以在vue3里面可以没有根标签

![1636697972(1).jpg](assets/97d17e33f76e43fba68e625543030905tplv-k3u1fbpfcp-watermark.awebp)





## 常用组合式API

### Composition API

和 Options API 的区别？

`Composition API` 也叫**组合式 API**，它主要就是为了解决 Vue2 中 Options API 的问题。

一是在 Vue2 中只能固定用 `data`、`computed`、`methods` 等选项组织代码，在组件越来越复杂的时候，一个功能相关的属性和方法就会在文件上中下到处都有，很分散，变越来越难维护

二是 Vue2 中虽然可以用 `minxin` 来做逻辑的提取复用，但是 minxin 里的属性和方法名会和组件内部的命名冲突，还有当引入多个 minxin 的时候，我们使用的属性或方法是来于哪个 minxin 也不清楚

而 `Composition API` 刚才就解决了这两个问题，可以让我们自由的组织代码，同一功能相关的全部放在一起，代码有更好的可读性更便于维护，单独提取出来也不会造成命名冲突，所以也有更好的可扩展性

### setup()

#### 定义

setup函数是 `Composition API`（组合API）的`入口`

#### 执行时机

setup `执行时机`是在 `beforeCreate` 之前执行，详细的可以看后面生命周期讲解。

```js
export default defineComponent({
  beforeCreate() {
    console.log("----beforeCreate----");
  },
  created() {
    console.log("----created----");
  },
  setup() {
    console.log("----setup----");
  },
});

```

![img](assets/cfa122fc38624892a1cfdd3efa14fdd6tplv-k3u1fbpfcp-watermark.awebp)

#### 使用方式

使用`setup`时，它接受两个参数：

1. props: 组件传入的属性
2. context



*// 方法* 

`setup(props, context) { return { name:'沐华' } } `

*// 语法糖* 

`<script setup> ... </script>`



在setup函数中定义的变量和方法最后都是需要 `return` 出去的 不然无法再模板中使用

```vue
<script>
 export default {
  name: 'App',
  setup(){
   let name = '流星'
   let age = 18
   //方法
   function say(){
    console.log(`我叫${name},今年${age}岁`)
   }

   //返回一个对象
   return {
    name,
    age,
    say
   }
  }
 }
</script>
```



这里兼容vue2的写法如：`data，methods...`，并且在vue2中可以读取到vue3里的配置但是vue3里面不能读取到vue2的配置，所以，vue3和vue2不要混用，如果有重名那么优先`setup`

#### 语法糖

##### 组件

```vue
<template>
  <div>
    <Foo />
  </div>
</template>

<!-- 在script标签上添加setup属性，以使用 script setup 语法 -->
<script setup>
  import Foo from './components/Foo.vue'
</script>
```

##### 属性和方法

```vue
<template>
  <div>
    <Foo />
    <h2 @click="increment">{{ count }}</h2>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import Foo from './components/Foo.vue'

  const count = ref(0)
  const increment = () => count.value++
</script>
```

上述案例会被编译为

```vue
<template>
  <div>
    <Foo />
    <h2 @click="increment">{{ count }}</h2>
  </div>
</template>

<script>
    // 导入的模块会被抽离到模块级别
    import { ref } from 'vue'
    import Foo from './components/Foo.vue'

    export default {
      setup() {
        const count = ref(0)
        const increment = () => count.value++

        // 这是一个返回h函数的render函数
        // 因为被编译到了setup函数中，所以可以直接访问顶层定义的属性和方法
        return () => ([
          h(Foo, null, ''),
          h('h2', {
            count,
            onClick: increment
          }, count)
        ])
      }
    }
</script>
```





##### props和emit





##### slots 和 attrs



##### 顶层await



##### 与普通 script 一起使用





### ref与reactive

#### ref



#### reactive







