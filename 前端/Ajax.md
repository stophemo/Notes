

# 原生AJAX

## AJAX简介

AJAX全称为Asynchronous JavaScript And XML，就是异步的JS和 XML。
通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势:无刷新获取数据。AJAX不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式。

## XML简介

XML可扩展标记语言。
XML被设计用来传输和存储数据。
XML和 HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据。

![image-20210722154059888](assets\image-20210722154059888.png)	

## AJAX的特点

### AJAX的优点

可以无需刷新页面与服务器端进行通信

允许你根据用户事件来更新部分页面内容

### AJAX的缺点

没有浏览历史，不能回退

存在跨域问题(同源)

SEO不友好

## AJAX的使用

### 安装node.js

### 安装express

### server.js

```js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
app.get('/server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应头
    response.send('HELLO AJAX')
});

//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动, 8000 端口监听中....");
});
```

### 请求的基本操作

GET

```html
	<button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName("button")[0];
        const textarea = document.getElementById("result");
        //绑定事件
        btn.onclick = function () {
            //1. 创建对象
            const xhr = new XMLHttpRequest();
            //2. 初始化 设置请求方法和 url
            xhr.open('GET', 'http://127.0.0.1:8000/server');
            //3. 发送
            xhr.send();
            //4. 事件绑定 处理服务端返回的结果
            // on  when 当....时候
            // readystate 是 xhr 对象中的属性, 表示状态 0 1 2 3 4
            // change  改变
            xhr.onreadystatechange = function () {
                //判断 (服务端返回了所有的结果)
                if (xhr.readyState === 4) {
                    //判断响应状态码 200  404  403 401 500
                    // 2xx 成功
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //处理结果  行 头 空行 体
                        //响应 
                        // console.log(xhr.status);//状态码
                        // console.log(xhr.statusText);//状态字符串
                        // console.log(xhr.getAllResponseHeaders());//所有响应头
                        // console.log(xhr.response);//响应体
                        //设置 result 的文本
                        result.innerHTML = xhr.response;
                    } else {

                    }
                }
            }
        }
    </script>
```

### 设置请求参数

```js
//2. 初始化 设置请求方法和 url
xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200&c=300');
```

### 发送POST请求

```html
    <div id="result"></div>
    <script>
        //获取元素对象
        const result = document.getElementById("result");
        //绑定事件
        result.addEventListener("mouseover", function () {
            //1. 创建对象
            const xhr = new XMLHttpRequest();
            //2. 初始化 设置类型与 URL
            xhr.open('POST', 'http://127.0.0.1:8000/server');
            //设置请求头
            // xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            // xhr.setRequestHeader('name', 'atguigu');
            //3. 发送
            xhr.send('a=100&b=200&c=300');
            // xhr.send('a:100&b:200&c:300');
            // xhr.send('1233211234567');

            //4. 事件绑定
            xhr.onreadystatechange = function () {
                //判断
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //处理服务端返回的结果
                        result.innerHTML = xhr.response;
                    }
                }
            }
        });
    </script>
```

server.js

```js
//创建路由规则
app.post('/server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //设置响应头
    response.send('HELLO AJAX POST')
});
```

### 设置请求头信息

```js
//2. 初始化 设置类型与 URL
xhr.open('POST', 'http://127.0.0.1:8000/server');
//设置请求头
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
//自定义         
xhr.setRequestHeader('name', 'atguigu');
//3. 发送
xhr.send('a=100&b=200&c=300');
```

解决自定义报错

```js
app.all('/server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //加上这句，再将app.post 改为app.all  可以接收任意类型的请求
    response.setHeader('Access-Control-Allow-Headers', '*');
    //设置响应头
    response.send('HELLO AJAX POST')
});
```

### 服务端响应JSON数据

```html
	<script>
        // 获取元素
        const result = document.getElementById("result");
        // 创建键盘点击事件
        window.onkeydown = function () {
            // 创建XMLHttpRequest对象
            const xhr = new XMLHttpRequest();
            // 设置响应数据的类型
            xhr.responseType = 'json';
            // 初始化
            xhr.open('GET', 'http://127.0.0.1:8000/json-server');
            // 发送
            xhr.send();
            // 事件绑定
            xhr.onreadystatechange = function () {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        // console.log(xhr.response);
                        // result.innerHTML = xhr.response;
                        // 1.对数据进行手动转换
                        // let data = JSON.parse(xhr.response);
                        // console.log(data);
                        // result.innerHTML = data.name;
                        // 2.自动转换
                        console.log(xhr.response);
                        result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
```

```js
app.all('/json-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // 响应一个数据
    const data = {
        name: 'jack'
    }
    // 对对象进行字符串转换
    let str = JSON.stringify(data);
    //设置响应体
    response.send(str);
});
```

### nodemon自动重启工具

https://www.npmjs.com/package/nodemon

安装指令

```
npm install -g nodemon
```

### IE缓存问题解决

在初始化设置请求url时加上当前时间

```js
xhr.open('GET', 'http://127.0.0.1:8000/ie?t=' + Date.now());
```

### 请求超时与网络异常处理

```js
btn.addEventListener('click', function () {
            const xhr = new XMLHttpRequest();
            // 超过两秒就取消请求
            xhr.timeout = 2000;
            // 超时回调 
            xhr.ontimeout = function () {
                alert("网络异常，请稍后重试！");
            }
            // 网络异常回调
            xhr.onerror = function () {
                alert("您的网络似乎出了点问题");
            }
            xhr.open('GET', 'http://127.0.0.1:8000/delay');
            xhr.send();
            xhr.onreadystatechange = function () {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
```

```js
//超时与网络异常
app.get('/delay', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    // 设置延时
    setTimeout(() => {
        //设置响应体
        response.send('延时响应');
    }, 3000);
});
```

### AJAX取消请求

```html
<button>发送请求</button>
    <button>取消发送</button>
    <script>
        const btn = document.querySelectorAll("button");
        let x = null;
        btn[0].addEventListener('click', function () {
            x = new XMLHttpRequest();
            x.open('GET', 'http://127.0.0.1:8000/delay');
            x.send();
        });
        //abort取消请求
        btn[1].addEventListener('click', function () {
            x.abort();
        });
    </script>
```

### 重复请求处理

```html
    <button>发送请求</button>
    <script>
        const btn = document.querySelector("button");
        let x = null;
        // 标识变量
        let isSending = false;
        btn.addEventListener('click', function () {
            if (isSending == true) {
                x.abort();
            }
            x = new XMLHttpRequest();
            isSending = true;
            x.open('GET', 'http://127.0.0.1:8000/delay');
            x.send();
            x.onreadystatechange = function () {
                if (x.readystate === 4) {
                    //修改标识变量
                    isSending = false;
                }
            }
        });
    </script>
```

# jQuery中的AJAX



## get请求

## post请求

## 通用方法ajax

$.ajax()的更多属性设置可以在jquery   API中查看

先引入jquery

```html
<link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css"
        rel="stylesheet">
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```

```html
<div class="container">
        <h2 class="page-header">jQuery发送AJAX请求 </h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
    <script>
        $('button').eq(0).click(function () {
            $.get('http://127.0.0.1:8000/jquery-server', { a: 100, b: 200 }, function (data) {
                console.log(data);
            }, 'json')
        })
        $('button').eq(0).click(function () {
            $.post('http://127.0.0.1:8000/jquery-server', { a: 100, b: 200 }, function (data) {
                console.log(data);
            })
        })
        $('button').eq(2).click(function () {
            $.ajax({
                //url
                url: 'http://127.0.0.1:8000/jquery-server',
                //参数
                data: { a: 100, b: 200 },
                //请求类型
                type: 'GET',
                //响应体结果
                dataType: 'json',
                //成功的回调
                success: function (data) {
                    console.log(data);
                },
                // 超时时间
                timeout: 3000,
                //失败的回调
                error: function () {
                    console.log('出错啦!!');
                },
                //头信息
                headers: {
                    c: 300,
                    d: 400
                }
            });
        });
    </script>
```

```js
//jquery 服务
app.all('/jquery-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    //设置响应体
    const data = { name: 'jack' };
    response.send(JSON.stringify(data));
});
```

# Axios发送ajax请求

## GET

## POST

## AJAX

```HTML
<button>GET</button>
    <button>POST</button>
    <button>AJAX</button>

    <script>
        // https://github.com/axios/axios
        const btns = document.querySelectorAll('button');

        //配置 baseURL
        axios.defaults.baseURL = 'http://127.0.0.1:8000';

        btns[0].onclick = function () {
            //GET 请求
            axios.get('/axios-server', {
                //url 参数
                params: {
                    id: 100,
                    vip: 7
                },
                //请求头信息
                headers: {
                    name: 'atguigu',
                    age: 20
                }
            }).then(value => {
                console.log(value);
            });
        }

        btns[1].onclick = function () {
            axios.post('/axios-server', {
                username: 'admin',
                password: 'admin'
            }, {
                //url 
                params: {
                    id: 200,
                    vip: 9
                },
                //请求头参数
                headers: {
                    height: 180,
                    weight: 180,
                }
            });
        }
        btns[2].onclick = function () {
            axios({
                //请求方法
                method: 'POST',
                //url
                url: '/axios-server',
                //url参数
                params: {
                    vip: 10,
                    level: 30
                },
                //头信息
                headers: {
                    a: 100,
                    b: 200
                },
                //请求体参数
                data: {
                    username: 'admin',
                    password: 'admin'
                }
            }).then(response => {
                //响应状态码
                console.log(response.status);
                //响应状态字符串
                console.log(response.statusText);
                //响应头信息
                console.log(response.headers);
                //响应体
                console.log(response.data);
            })
        }
    </script>
```

```JS
//axios 服务
app.all('/axios-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = { name: '尚硅谷' };
    response.send(JSON.stringify(data));
});
```

# fetch函数发送AJAX请求

```html
    <button>AJAX请求</button>
    <script>
        //文档地址
        //https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch

        const btn = document.querySelector('button');
        //fetch函数返回的promise对象
        btn.onclick = function () {
            fetch('http://127.0.0.1:8000/fetch-server?vip=10', {
                //请求方法
                method: 'POST',
                //请求头
                headers: {
                    name: 'atguigu'
                },
                //请求体
                body: 'username=admin&password=admin'
            }).then(response => {
                // return response.text();
                return response.json();
            }).then(response => {
                console.log(response);
            });
        }
    </script>
```

```js
//fetch 服务
app.all('/fetch-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = { name: '尚硅谷' };
    response.send(JSON.stringify(data));
});

```

# 跨域

## 同源策略

同源策略(Same-Origin Policy)最早由 Netscape 公司提出，是浏览器的一种安全策略

同源： 协议、域名、端口号 必须完全相同。 违背同源策略就是跨域。

## 如何解决跨域

### JSONP

#### JSONP 是什么 

JSONP(JSON with Padding)，是一个非官方的跨域解决方案，纯粹凭借程序员的聪明 才智开发出来，只支持 get 请求。

#### JSONP 怎么工作的？

 在网页有一些标签天生具有跨域能力，比如：img link iframe script。 JSONP 就是利用 script 标签的跨域能力来发送请求的

#### JSONP实现原理

```html
    <div id="result"></div>
    <script>
        //处理数据
        function handle(data) {
            //获取 result 元素
            const result = document.getElementById('result');
            result.innerHTML = data.name;
        }
    </script>
    <!-- <script src="http://127.0.0.1:5500/%E8%AF%BE%E5%A0%82/%E4%BB%A3%E7%A0%81/7-%E8%B7%A8%E5%9F%9F/2-JSONP/js/app.js"></script> -->
    <script src="http://127.0.0.1:8000/jsonp-server"></script>
```

app.js

```js
const data = {
    name: '尚硅谷atguigu'
};

handle(data);
```

#### JSONP实践

```html
    用户名: <input type="text" id="username">
    <p></p>
    <script>
        //获取 input 元素
        const input = document.querySelector('input');
        const p = document.querySelector('p');
        
        //声明 handle 函数
        function handle(data){
            input.style.border = "solid 1px #f00";
            //修改 p 标签的提示文本
            p.innerHTML = data.msg;
        }

        //绑定事件
        input.onblur = function(){
            //获取用户的输入值
            let username = this.value;
            //向服务器端发送请求 检测用户名是否存在
            //1. 创建 script 标签
            const script = document.createElement('script');
            //2. 设置标签的 src 属性
            script.src = 'http://127.0.0.1:8000/check-username';
            //3. 将 script 插入到文档中
            document.body.appendChild(script);
        }
    </script>
```



```js
//用户名检测是否存在
app.all('/check-username',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        exist: 1,
        msg: '用户名已经存在'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
```



#### jquery-jsonp

先引入jquery

```html
    <button>点击发送 jsonp 请求</button>
    <div id="result">

    </div>
    <script>
        $('button').eq(0).click(function(){
            $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function(data){
                $('#result').html(`
                    名称: ${data.name}<br>
                    校区: ${data.city}
                `)
            });
        });
    </script>
```



```js
//jQuery-jsonp 服务
app.all('/jquery-jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name:'尚硅谷',
        city: ['北京','上海','深圳']
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //接收 callback 参数
    let cb = request.query.callback;

    //返回结果
    response.end(`${cb}(${str})`);
});
```



### CORS

#### MDN文档链接

[跨源资源共享（CORS） - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)

#### CORS 是什么？

 CORS（Cross-Origin Resource Sharing），跨域资源共享。CORS 是官方的跨域解决方 案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持 get 和 post 请求。跨域资源共享标准新增了一组 HTTP 首部字段，允许服务器声明哪些 源站通过浏览器有权限访问哪些资源 

#### CORS 怎么工作的？ 

CORS 是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应 以后就会对响应放行

```html
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            //1. 创建对象
            const x = new XMLHttpRequest();
            //2. 初始化设置
            x.open("GET", "http://127.0.0.1:8000/cors-server");
            //3. 发送
            x.send();
            //4. 绑定事件
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        //输出响应体
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
```



```JS
app.all('/cors-server', (request, response)=>{
    //设置响应头
    response.setHeader("Access-Control-Allow-Origin", "*");
    response.setHeader("Access-Control-Allow-Headers", '*');
    response.setHeader("Access-Control-Allow-Method", '*');
    // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
    response.send('hello CORS');
});
```

































































# +++

## Chrome调试

F12   network   XHR  对AJAX请求的筛选



## readystate

 0 － （未初始化）还没有调用send()方法
 1 － （载入）已调用send()方法，正在发送请求
 2 － （载入完成）send()方法执行完成，已经接收到全部响应内容
 3 － （交互）正在解析响应内容
 4 － （完成）响应内容解析完成，可以在客户端调用了







