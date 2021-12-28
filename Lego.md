## Lego memorandum

### Gitlab

`username: cn8NanHu`
`p:  Welcome12345678`

### Lego login

`userName: lingcsy1983@aliyun.com`

`password:4510679560228883`

`code:20211234`

## useState,useEffect

函数组件代替 class 组件，函数组件还是会面临**两个问题**：

- 函数组件没有 state  ----`useState()`
- 函数组件没有生命周期  -----`useEffect()`

```react
const [n, setN] = React.useState(0);
const [n, setN] = React.useState(()=>{
	console.log('这里也可以是一个函数')	
})
//useState()返回一个数组，第一个是读，第二个是写
//useState()里的函数只会执行一次，即使组件再渲染
```

```react
useEffect(()=>{
  console.log('第一个参数是函数')
},[n])
// useEffect() 方法接收两个参数，第一个参数是函数，
// 第二个参数的设置决定useEffect()模拟的生命钩子
```

### useState()

#### state

State是一个组件的UI数据模型，是组件渲染时的数据依据，state是私有的，可以认为state是组件的`私有属性`

#### State 的更新是异步的

- 调用setState后，setState会把要修改的状态放入一个队列中（因而 组件的state并不会立即改变）；
- 之后React 会优化真正的执行时机，来优化性能，所以优化过程中有可能会将多个 setState 的状态修改合并为一次状态修改，因而state更新是异步的。
- 所以不要依赖当前的State，计算下个State。当真正执行状态修改时，依赖的this.state并不能保证是最新的State，因为React会把多次State的修改合并成一次，这时，this.state将还是这几次State修改前的State。
- 另外需要注意的是，同样不能依赖当前的Props计算下个状态，因为Props一般也是从父组件的State中获取，依然无法确定在组件状态更新时的值。

#### useState做了哪些事？

```react
 const Demo = ()=> {
      const [n,setN] = React.useState(0)
      return <div>
        {n}
        <button onClick={()=> {setN(n+1)}}>点我+1</button>
      </div>
    }
    const rootElement = document.getElementById("app")
    ReactDOM.render(<Demo />, rootElement);
```

首次渲染：

render()------得到Demo组件------调用Demo组件------得到虚拟div------创建真实的div

点击button后：

调用setN(n+1)------再次render()------得到Demo组件------调用Demo组件------得到虚拟div------使用DOM Diff对比------更新真实的div

### useEffect()

模拟生命周期

- 模拟 `componentDidMount`：

  *第一次渲染时*

  useEffect((）=> {console.log（'第一次渲染）}，[ ]）。第二个参数为**空数组**

- 模拟 `componentDidUpdate`：

  ​		*数据变更时调用*

  - useEffect((）=> {console.log（'任意属性变更）}。第二个参数为**空**（监听所有state）
  - useEffect((）=> {console.log（'n变了‘）}，[n]）。第二个参数为要组件上的**变量**。（监听这个变量）

- 模拟 `componentWillUnmount`：

  *组件将要销毁时*

  useEffect() 的第一个参数的返回的是函数时，会在组件要销毁时调用。

- 模拟 `constructor`：

  *初始化时调用*

  函数组件在使用 useState() 声明变量，声明组件中的函数，就相当于类组件的 constructor。

## Promise

promise是异步编程的一种解决方案

语法上：Promise是一个对象，可以获取异步操作的消息

本   意：承诺，一段时间给出一个结果

Promise有三种状态：

`pending(等待态)`    `fulfiled(成功态)`   `rejected(失败态)`

状态一旦改变，就不会再变

Promise实例创建后 会`立即执行`，无法中途取消

### 解决的问题

- `回调地狱`，代码难以维护， 常常第一个的函数的输出是第二个函数的输入这种现象
- promise可以支持多个`并发的请求`，获取并发请求中的数据
- 这个promise可以解决`异步`的问题，本身不能说promise是异步的

### 基本用法

`resolve`函数的作用是，将`Promise`对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去

`reject`函数的作用是，将`Promise`对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

`then`方法可以接受两个回调函数作为参数。

- 第一个回调函数是`Promise`对象的状态变为`resolved`时调用
- 第二个回调函数是`Promise`对象的状态变为`rejected`时调用。
- 这两个函数都是可选的，不一定要提供。
- 它们都接受`Promise`对象传出的值作为参数。





## HTTP请求状态码

![http状态码](C:\Users\jiehuo\Documents\Office\documents\http状态码.png)



## 挂载

*将组件渲染，并且构造 DOM 元素然后塞入页面的过程称为组件的挂载*