####  输入输出语句

![image-20210712203017634](assets\image-20210712203017634.png)

#### 变量

​	 不声明，直接赋值使用，会变成全局变量。

#### 数据类型

![image-20210712204041614](assets\image-20210712204041614.png)

##### 数字型

![image-20210712204616952](assets\image-20210712204616952.png)

![image-20210712204731557](assets\image-20210712204731557.png)

##### 字符串型

![image-20210712204841138](assets\image-20210712204841138.png)

![image-20210712205017383](assets\image-20210712205017383.png)

![image-20210712205301947](assets\image-20210712205301947.png)

##### 布尔型

##### undefined

##### null

![image-20210712205643876](assets\image-20210712205643876.png)

**typeof 可以检测数据类型**

<img src="assets\image-20210712205952207.png" alt="image-20210712205952207" style="zoom:50%;" />	

##### 复杂数据类型：Object 对象     数组

#### 简单数据类型和复杂数据类型

##### 简单数据类型：

简单类型又叫做基本数据类型或者值类型，复杂类型又叫做引用类型。

值类型∶简单数据类型/基本数据类型，在存储时变量中存储的是值本身，因此叫做值类型
string , number , boolean , undefined , null

![image-20210718155259672](assets\image-20210718155259672.png)	

##### 栈与堆

堆栈空间分配区别:
1、栈（操作系统）︰

由操作系统自动分配释放存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈;

简单数据类型存放到栈里面

2、堆(操作系统）∶

存储复杂类型(对象)，一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。

复杂数据类型存放到堆里面

JavaScript中没有堆栈的概念，通过堆栈的方式，可以让大家更容易理解代码的一些执行方式

##### 内存分配

<img src="assets\image-20210718160143813.png" alt="image-20210718160143813" style="zoom: 67%;" />	

##### 简单数据类型传参

函数的形参也可以看做是一个变量，当我们把一个值类型变量作为参数传给函数的形参时，其实是把变量在栈空间里的值复制了一份给形参，那么在方法内部对形参做任何修改，都不会影响到的外部变量。

e.g

![image-20210718162328750](assets\image-20210718162328750.png)	   		x的值没变

##### 复杂数据类型传参

函数的形参也可以看做是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存的堆地址复制给了形参，形参和实参其实保存的是同一个堆地址，所以操作的是同一个对象。

e.g

​	<img src="assets\image-20210718162242634.png" alt="image-20210718162242634" style="zoom: 80%;" />	p.name:刘德华    ——》  p.name: 张学友

#### 数据类型转换

##### 转为字符串型

![image-20210713132526828](assets\image-20210713132526828.png)

##### 转为数字型

![image-20210713132859615](assets\image-20210713132859615.png)

**计算年龄案例**

![image-20210713133246556](assets\image-20210713133246556.png)

**简单加法案例**

![image-20210713133730592](assets\image-20210713133730592.png)

##### 转化为布尔型

![image-20210713134006535](assets\image-20210713134006535.png)



#### 扩展阅读

##### 解释型语言和编译型语言

![image-20210713134222148](assets\image-20210713134222148.png)

##### 标识符、关键字、保留字

标识(zhi)符∶就是指开发人员为变量、属性、函数、参数取的名字。

标识符不能是关键字或保留字。

关键字∶是指JS本身已经使用了的字，不能再用它们充当变量名、方法名。
包括: break、case、catch、continue、default、delete、do、else、finally、for、function、if、in、instanceof、new、return、switch、this、throw、try、typeof、var、void、while、with等。

3.保留字
保留字∶实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。
包括: boolean、byte、char、class、const、debugger、double、enum、export、extends、fimal、float、goto、implements、import、int、interface、long、mative、package、private、protected、public、 short、static、super、synchronized、throws、transient、volatile等。



#### 运算符

##### --与++

![image-20210714094139207](assets\image-20210714094139207.png)

##### 比较运算符

![image-20210714094603161](assets\image-20210714094603161.png)

##### 逻辑运算符

![image-20210714094750261](assets\image-20210714094750261.png)

##### 短路运算

![image-20210714095556956](assets\image-20210714095556956.png)

#### 流程控制

##### 循环

##### 三元表达式

数字补 0 案例

![image-20210714101830100](assets\image-20210714101830100.png)

##### switch

![image-20210714102014718](assets\image-20210714102014718.png)

##### switch与if...else的区别

![image-20210714102314437](assets\image-20210714102314437.png)

#### 断点调试

F12 - sources - 行号 - ...

#### 循环

##### for循环

###### 打印倒三角案例

```js
var str = "";
        for (var i = 0; i < 10; i++) {
            for (var j = i; j < 10; j++) {
                str += '*';
            }
            str += '\n';
        }
        console.log(str);
```

###### 打印九九乘法表

```javascript
var str = '';
        for (var i = 1; i < 10; i++) {
            for (var j = 1; j <= i; j++) {
                str += j + 'x' + i + '=' + i * j + '\t';
            }
            str += '\n';
        }
        console.log(str);
```

##### while循环

##### do while循环

##### continue

跳过本次循环，执行i++

##### break

跳出整个循环

#### 数组

##### 1.概念

##### 2.创建数组

```js
//1.new
var arr = new Array();
//2.利用数组字面量
var arr = []; 
```

##### 3.获取数组中的元素

```js
arr[index]
```

##### 4.遍历数组

```js
for (var i = 0; i < arr.length; i++){
	console.log(arr[i]);
}
```

###### 案例1 ：从数组中取出最大值

```js
var arr = [2,6,1,77,52,25,7];
var max = arr[0];
for (var i =1; i<arr.length ; i++){
    if(arr[i]>max) {
        max = arr[i];
    }
}
```

###### 案例2：数组转换为分割字符串

##### 5.数组中新增元素

![image-20210717105956475](assets\image-20210717105956475.png)

![image-20210717110052763](assets\image-20210717110052763.png)

##### 6.数组案例

**筛选数组**

方法一：

![image-20210717134813463](assets\image-20210717134813463.png)

方法二：

用	.length  代表新数组下标

![image-20210717134945909](assets\image-20210717134945909.png)

**数组去重**

![image-20210717135252320](assets\image-20210717135252320.png)

**翻转数组**

![image-20210717135528535](assets\image-20210717135528535.png)



##### 7.数组方法

###### find（）

```js
var ages = [3, 10, 18, 20];
 
function checkAdult(age) {
    return age >= 18;
}
 
function myFunction() {
    document.getElementById("demo").innerHTML = ages.find(checkAdult);
}
```



#### 排序

##### 1.冒泡排序

![image-20210717141709653](assets\image-20210717141709653.png)

![image-20210718082706094](D:\Typora\前端笔记\前端\JavaScript.assets\image-20210718082706094.png)	

#### 函数

##### 1.概念

##### 2.使用

##### 3.参数

###### 形参

形式上的参数 函数定义的时候传递的参数 当前并不知道是什么

形参类似变量，但是不用声明

形参是接受实参的

###### 实参

实际上的参数 函数调用 的时候传递的参数 实参是传递给形参的

##### 形参与实参个数不匹配问题

![image-20210717143259054](assets\image-20210717143259054.png)

##### 4.返回值

返回给当前调用者

![image-20210717144245969](assets\image-20210717144245969.png)

![image-20210717144315842](assets\image-20210717144315842.png)

函数都是有返回值的
1．如果有return则返回return后面的值

2．如果没有return则返回undefined

##### 5.arguments的使用

![image-20210717144802314](assets\image-20210717144802314.png)

![image-20210717145139545](assets\image-20210717145139545.png)

##### 6.函数案例

![image-20210717145449767](assets\image-20210717145449767.png)	

![image-20210717145716539](assets\image-20210717145716539.png)	

##### 7.两种声明方式

![image-20210717154346645](assets\image-20210717154346645.png)

#### 作用域

![image-20210717163826114](assets\image-20210717163826114.png)

![image-20210717163917127](assets\image-20210717163917127.png)	

![image-20210717164033529](assets\image-20210717164033529.png)	

![image-20210717164631411](assets\image-20210717164631411.png)

##### 作用域链

<img src="assets\image-20210717164827422.png" alt="image-20210717164827422" style="zoom:67%;" />	

#### js预解析

##### 1.预解析

![image-20210717170350847](assets\image-20210717170350847.png)

##### 2.变量预解析和函数预解析

##### 3.预解析案例

![image-20210717171109510](assets\image-20210717171109510.png)	

输出：  undefined

![image-20210717171308468](assets\image-20210717171308468.png)	

输出： undefined  

​			 20

![image-20210717171522706](assets\image-20210717171522706.png)	

输出： undefined 

​			9

![image-20210717171546601](assets\image-20210717171546601.png)	 

![image-20210717172630827](assets\image-20210717172630827.png)

输出：

<img src="assets\image-20210717172814875.png" alt="image-20210717172814875" style="zoom:50%;" />



#### 对象

##### 概念

![image-20210717173318925](assets\image-20210717173318925.png)

##### 对象创建的三种方式

###### 利用字面量创建对象

![image-20210717173605704](assets\image-20210717173605704.png)

使用：![image-20210717173708284](assets\image-20210717173708284.png)

###### 利用new Object 创建对象

![image-20210717174212586](assets\image-20210717174212586.png)

使用同上

###### 利用构造函数创建对象

![image-20210717175027503](assets\image-20210717175027503.png)





![image-20210717174729823](assets\image-20210717174729823.png)

![image-20210717175640295](assets\image-20210717175640295.png)

##### 遍历对象

![image-20210717175955062](assets\image-20210717175955062.png)

##### 小结

![image-20210717180345405](assets\image-20210717180345405.png)

#### js内置对象

##### 1.简介

JavaScript中的对象分为3种∶自定义对象、内置对象、浏览器对象

前面两种对象是JS基础内容，属于ECMAScript;第三个浏览器对象属于我们JS独有的，我们JSAPI讲解

内置对象就是指JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能(属性和方法)

内置对象最大的优点就是帮助我们快速开发

JavaScript提供了多个内置对象:Math、 Date . Array、string等

##### 2.查MDN文档

**MDN**

##### 3.Math对象

![image-20210717205510795](assets\image-20210717205510795.png)

![image-20210717204615282](assets\image-20210717204615282.png)

![image-20210717205606205](assets\image-20210717205606205.png)4

![image-20210717205712862](assets\image-20210717205712862.png)

![image-20210717210549657](assets\image-20210717210549657.png)

![image-20210717212018110](assets\image-20210717212018110.png)

###### **猜数字案例**

```js
  function game(min, max, number) {
            var random = Math.floor(Math.random() * (max - min + 1)) + min;
            for (var i = 1; i <= number + 1; i++) {
                if (i == number + 1) {
                    alert("机会用完了哦！！！");
                    break;
                }
                var num = prompt("请输入" + min + "-" + max + "之间的整数,只有" + number + "次机会哦！！！");
                if (num > random) {
                    alert("猜大了！！！");
                }
                else if (num < random) {
                    alert("猜小了！！！");
                }
                else if (num == random) {
                    alert("猜对了！！！");
                    break;
                }
            }
        }
        game(1, 10, 5);
```



##### 4.日期对象

![image-20210717220922685](assets\image-20210717220922685.png)

![image-20210717221043381](assets\image-20210717221043381.png)

![image-20210717221413312](assets\image-20210717221413312.png)

###### **格式化时分秒：**

![image-20210717221913778](assets\image-20210717221913778.png)

![image-20210717222240134](assets\image-20210717222240134.png)

###### **倒计时**

![image-20210718075141494](assets\image-20210718075141494.png)	

![image-20210718075237556](assets\image-20210718075237556.png)	



##### 5.数组对象

###### **创建数组**

![image-20210718075446106](assets\image-20210718075446106.png)	

![image-20210718075504946](assets\image-20210718075504946.png)

###### **是否数组**

![image-20210718080114076](assets\image-20210718080114076.png)	

###### **添加或删除数组**

![image-20210718080515259](assets\image-20210718080515259.png) 

###### **筛选数组**

```js
new Arr[newArr.length] = arr[i];
```

//可以替换为

```js
newArr.push(arr[i]);
```

###### **数组排序**

![image-20210718082706094](assets\image-20210718082706094.png)	

**sort()**

默认按个位数排序

```js
Arry.sort(function(a,b){
    return a-b;//升序
})
```

也可以这样写

```js
Arry.sort((a, b) => a - b);
```

###### **数组索引方法**

![image-20210718083845871](assets\image-20210718083845871.png)

**indexOf()**

从前面开始查找

**lastIndexOf()**

从后面开始查找

###### **数组去重案例**

![image-20210718084748375](assets\image-20210718084748375.png)

###### 数组 -> 字符串

![image-20210718085126109](assets\image-20210718085126109.png)	

###### 补充**数组对象操作**

![image-20210718085157893](assets\image-20210718085157893.png)	

​	

##### 6.字符串对象

###### 基本包装类型

![image-20210718090306641](assets\image-20210718090306641.png)	

###### 字符的不可变性

指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

###### 案例：查找字符串中某个字符出现的位置以及次数

![image-20210718091316471](assets\image-20210718091316471.png)

###### 根据索引号返回指定字符

![image-20210718091704706](assets\image-20210718091704706.png)

###### 统计出现次数最多的字符

![image-20210718093823681](assets\image-20210718093823681.png)	

![image-20210718093902097](assets\image-20210718093902097.png)	

###### 拼接以及截取字符串

![image-20210718150223018](assets\image-20210718150223018.png)

###### 其他方法

**replace()**

![image-20210718150548059](assets\image-20210718150548059.png)

**split()**

![image-20210718150800542](assets\image-20210718150800542.png)

转换大小写

![image-20210718150822304](assets\image-20210718150822304.png)



#### API

##### API

APl ( Application Programming Interface,应用程序编程接口)是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无雾访问源码，或理解内部工作机制的细节。

##### JS的组成

<img src="assets\image-20210718162652648.png" alt="image-20210718162652648" style="zoom:50%;" />	

##### Web API

![image-20210718163020561](assets\image-20210718163020561.png)	

#### DOM

##### 简介

![image-20210718163602630](assets\image-20210718163602630.png)	

##### 获取元素

###### 根据id获取

getElementById

![image-20210718165825131](assets\image-20210718165825131.png)

getElementsByTagName

![image-20210718170515742](assets\image-20210718170515742.png)

###### H5新增获取元素方式

![image-20210718170746491](assets\image-20210718170746491.png)

###### 获取body   html  元素

![image-20210718170920514](assets\image-20210718170920514.png)

##### 事件

###### 概述

![image-20210718171130001](assets\image-20210718171130001.png)

###### 事件三要素

![image-20210718171235811](assets\image-20210718171235811.png)

执行

##### 操作元素

###### 改变元素内容

![image-20210718171804728](assets\image-20210718171804728.png)

###### 改变元素属性

![image-20210718172247844](assets\image-20210718172247844.png)

###### H5自定义属性

![image-20210719123053347](assets\image-20210719123053347.png)



###### 分时间显示不同图片案例

![image-20210718172740301](assets\image-20210718172740301.png)

###### 修改表单属性

表单里面的值或者文字内容是通过 value 来修改的

###### 仿京东密码显示隐藏案例

![image-20210718173558103](assets\image-20210718173558103.png)

###### 样式属性操作

![image-20210718173749091](assets\image-20210718173749091.png)

###### 关闭淘宝二维码案例

![image-20210718174040999](assets\image-20210718174040999.png)

###### 循环精灵图

```js
var lis = document.querySelectorAll( 'li');
for (var i = 0; i<lis.length; i++){
//让索引号乘以44就是每个li的背景y坐标index就是我们的y坐标
    var index = i * 44;
    lis[i].style.backgroundPosition = 
        "0 -"+index+"px";
}
```

###### 通过className修改样式属性

![image-20210718180027826](assets\image-20210718180027826.png)

###### 案例：密码框验证信息

 ![image-20210718180419503](assets\image-20210718180419503.png)

###### 总结：

![image-20210718180549643](assets\image-20210718180549643.png)

##### DOM重点核心

关于dom操作，我们主要针对于元素的操作。主要有创建、增、删、改、查、属性操作、事件操作。

###### 创建

![image-20210719141521800](assets\image-20210719141521800.png)	

###### 增

![image-20210719141533561](assets\image-20210719141533561.png)	

###### 删

![image-20210719141542639](assets\image-20210719141542639.png)	

###### 改

![image-20210719141552759](assets\image-20210719141552759.png)

###### 查

![image-20210719141628881](assets\image-20210719141628881.png)

###### 属性操作

![image-20210719141656875](assets\image-20210719141656875.png)

###### 事件操作

![image-20210719141715750](assets\image-20210719141715750.png)

#### 排他思想

##### 介绍

![image-20210718181120195](assets\image-20210718181120195.png)

##### 百度换肤效果

![image-20210718181736341](assets\image-20210718181736341.png)

##### 表格隔行变色

![image-20210719112959577](assets\image-20210719112959577.png)

##### 全选反选

![image-20210719113446367](assets\image-20210719113446367.png)

![image-20210719113905142](assets\image-20210719113905142.png)

#### 节点操作

![image-20210719123237973](assets\image-20210719123237973.png)

##### 概述

![image-20210719123256469](assets\image-20210719123256469.png)

##### 父级节点

![image-20210719123749322](assets\image-20210719123749322.png)	

##### 子级节点

![image-20210719124741102](assets\image-20210719124741102.png)	

![image-20210719125011046](assets\image-20210719125011046.png)	

##### 案例： 下拉菜单

![image-20210719125453822](assets\image-20210719125453822.png)	

![image-20210719125427020](assets\image-20210719125427020.png)	

##### 兄弟节点

![image-20210719125746475](assets\image-20210719125746475.png)	

第二种  IE9以上才支持

###### 封装兼容性函数

<img src="assets\image-20210719125656839.png" alt="image-20210719125656839" style="zoom:50%;" />	

##### 创建和添加元素

![image-20210719130149144](assets\image-20210719130149144.png)	

##### 案例：发布留言案例

![image-20210719130500385](assets\image-20210719130500385.png)	

##### 删除节点

![image-20210719130645944](assets\image-20210719130645944.png)	

##### 案例：删除留言案例

![image-20210719131053715](assets\image-20210719131053715.png)		![image-20210719131109145](assets\image-20210719131109145.png)

##### 克隆节点

![image-20210719131344104](assets\image-20210719131344104.png)	

##### 案例：动态生成表格

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        table {
            width: 500px;
            margin: 100px auto;
            border-collapse: collapse;
            text-align: center;
        }

        td,
        th {
            border: 1px solid #333;
        }

        thead tr {
            height: 40px;
            background-color: #ccc;
        }
    </style>
</head>

<body>
    <table cellspacing="0">
        <thead>
            <tr>
                <th>姓名</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>

        </tbody>
    </table>
    <script>
        // 1.先去准备好学生的数据
        var datas = [{
            name: '魏璎珞',
            subject: 'JavaScript',
            score: 100
        }, {
            name: '弘历',
            subject: 'JavaScript',
            score: 98
        }, {
            name: '傅恒',
            subject: 'JavaScript',
            score: 99
        }, {
            name: '明玉',
            subject: 'JavaScript',
            score: 88
        }, {
            name: '大猪蹄子',
            subject: 'JavaScript',
            score: 0
        }];
        // 2. 往tbody 里面创建行： 有几个人（通过数组的长度）我们就创建几行
        var tbody = document.querySelector('tbody');
        for (var i = 0; i < datas.length; i++) { // 外面的for循环管行 tr
            // 1. 创建 tr行
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            // 2. 行里面创建单元格(跟数据有关系的3个单元格) td 单元格的数量取决于每个对象里面的属性个数  for循环遍历对象 datas[i]
            for (var k in datas[i]) { // 里面的for循环管列 td
                // 创建单元格 
                var td = document.createElement('td');
                // 把对象里面的属性值 datas[i][k] 给 td  
                // console.log(datas[i][k]);
                td.innerHTML = datas[i][k];
                tr.appendChild(td);
            }
            // 3. 创建有删除2个字的单元格 
            var td = document.createElement('td');
            td.innerHTML = '<a href="javascript:;">删除 </a>';
            tr.appendChild(td);

        }
        // 4. 删除操作 开始 
        var as = document.querySelectorAll('a');
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function () {
                // 点击a 删除 当前a 所在的行(链接的爸爸的爸爸)  node.removeChild(child)  
                tbody.removeChild(this.parentNode.parentNode)
            }
        }
        // for(var k in obj) {
        //     k 得到的是属性名
        //     obj[k] 得到是属性值
        // }
    </script>
</body>

</html>
```

##### 三种动态创建元素的区别

![image-20210719141143656](assets\image-20210719141143656.png)	

#### 事件高级

##### 注册事件（绑定事件)

###### 概述

![image-20210719142219814](assets\image-20210719142219814.png)

###### 方法监听注册事件

![image-20210719142301150](assets\image-20210719142301150.png)	

###### IE9 attachEvent

![image-20210719142753974](assets\image-20210719142753974.png)	

###### 兼容性处理方案

<img src="assets\image-20210719142935283.png" alt="image-20210719142935283" style="zoom: 67%;" />	

##### 删除事件（解绑事件)

###### 传统方式

![image-20210719143317304](assets\image-20210719143317304.png)	

###### 方法监听注册方式

![image-20210719143326907](assets\image-20210719143326907.png)	

##### DOM事件流

###### 原理

<img src="assets\image-20210719143742857.png" alt="image-20210719143742857" style="zoom: 67%;" />	

<img src="assets\image-20210719143805221.png" alt="image-20210719143805221" style="zoom:50%;" />	

###### 注意事项

<img src="assets\image-20210719144512672.png" alt="image-20210719144512672" style="zoom: 80%;" />	

##### 事件对象

###### 简介

![image-20210719151348491](assets\image-20210719151348491.png)	

###### 常见属性和方法

![image-20210719151559876](assets\image-20210719151559876.png)

###### this和 e.target 的区别

![image-20210719151826279](assets\image-20210719151826279.png)





##### 阻止事件冒泡

###### 组织冒泡两种写法

![image-20210719152605406](assets\image-20210719152605406.png)	

###### 兼容方案

![image-20210719152713821](assets\image-20210719152713821.png)	



##### 事件委托(代理、委派)常用的鼠标事件

###### 原理

<img src="assets\image-20210719153031323.png" alt="image-20210719153031323" style="zoom: 80%;" />	

###### 代码实现

```html
<ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
        })
    </script>
```

##### 常用的鼠标事件

![image-20210719153304848](assets\image-20210719153304848.png)	

![image-20210719153844887](assets\image-20210719153844887.png)	

###### 补充

```html
<body>
    我是一段不愿意分享的文字
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
            })
            // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function(e) {
            e.preventDefault();
        })
    </script>
</body>
```

###### 案例：跟随鼠标的图片

```html
<style>
        img {
            position: absolute;
            top: 2px;
        }
</style>

<img src="images/angel.gif" alt="">
    <script>
        var pic = document.querySelector('img');
        document.addEventListener('mousemove', function(e) {
            // 1. mousemove只要我们鼠标移动1px 就会触发这个事件
            // console.log(1);
            // 2.核心原理： 每次鼠标移动，我们都会获得最新的鼠标坐标， 把这个x和y坐标做为图片的top和left 值就可以移动图片
            var x = e.pageX;
            var y = e.pageY;
            console.log('x坐标是' + x, 'y坐标是' + y);
            //3 . 千万不要忘记给left 和top 添加px 单位
            pic.style.left = x - 50 + 'px';
            pic.style.top = y - 40 + 'px';
        });
    </script>
```



##### 常用的键盘事件

###### 常用

![image-20210720082218621](assets\image-20210720082218621.png)	

###### 键盘事件对象

![image-20210720082536677](assets\image-20210720082536677.png)	

```js
// 键盘事件对象中的keyCode属性可以得到相应键的ASCII码值
        // 1. 我们的keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
        // 2. 我们的keypress 事件 区分字母大小写  a  97 和 A 得到的是65
        document.addEventListener('keyup', function(e) {
            // console.log(e);
            console.log('up:' + e.keyCode);
            // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
            if (e.keyCode === 65) {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }

        })
        document.addEventListener('keypress', function(e) {
            // console.log(e);
            console.log('press:' + e.keyCode);

        })
```

###### 案例：模拟京东快递单号查询

```js
<div class="search">
        <div class="con">123</div>
        <input type="text" placeholder="请输入您的快递单号" class="jd">
    </div>
    <script>
        // 快递单号输入内容时， 上面的大号字体盒子（con）显示(这里面的字号更大）
        // 表单检测用户输入： 给表单添加键盘事件
        // 同时把快递单号里面的值（value）获取过来赋值给 con盒子（innerText）做为内容
        // 如果快递单号里面内容为空，则隐藏大号字体盒子(con)盒子
        var con = document.querySelector('.con');
        var jd_input = document.querySelector('.jd');
        jd_input.addEventListener('keyup', function() {
                // console.log('输入内容啦');
                if (this.value == '') {
                    con.style.display = 'none';
                } else {
                    con.style.display = 'block';
                    con.innerText = this.value;
                }
            })
            // 当我们失去焦点，就隐藏这个con盒子
        jd_input.addEventListener('blur', function() {
                con.style.display = 'none';
            })
            // 当我们获得焦点，就显示这个con盒子
        jd_input.addEventListener('focus', function() {
            if (this.value !== '') {
                con.style.display = 'block';
            }
        })
    </script>
```



#### BOM

##### 什么是BOM![image-20210720084210487](assets\image-20210720084210487.png)	

##### BOM的构成

![image-20210720084608107](assets\image-20210720084608107.png)	

##### 常见事件

###### onload

```js
window.addEventListener('load', function() {
	alert(22);
})
document.addEventListener('DOMContentLoaded', function() {
	alert(33);
})
// load 等页面内容全部加载完毕，包含页面dom元素 图片 flash  css 等等
// DOMContentLoaded 是DOM 加载完毕，不包含图片 falsh css 等就可以执行 加载速度比 load更快一些
```

###### resize

<img src="assets\image-20210720085322699.png" alt="image-20210720085322699" style="zoom: 67%;" />	

```js
<script>
        window.addEventListener('load', function() {
            var div = document.querySelector('div');
            window.addEventListener('resize', function() {
                console.log(window.innerWidth);

                console.log('变化了');
                if (window.innerWidth <= 800) {
                    div.style.display = 'none';
                } else {
                    div.style.display = 'block';
                }

            })
        })
</script>
```

##### 定时器

###### 回调函数

setTimeout()这个调用函数我们也称为`回调函数callback`

普通函数是按照代码顺序直接调用。而这个函数，需要等待时间，时间到了才去调用这个函数，因此称为回调函数。

简单理解︰回调，就是回头调用的意思。上一件事千完，再回头再调用这个函数。

以前我们讲的` element.onclick =function()A}`或者`element.addEventListener("click" , fn);`里面的函数也是回调函数。

###### setTimeout()

```js
// 1. setTimeout 
        // 语法规范：  window.setTimeout(调用函数, 延时时间);
        // 1. 这个window在调用的时候可以省略
        // 2. 这个延时时间单位是毫秒 但是可以省略，如果省略默认的是0
        // 3. 这个调用函数可以直接写函数 还可以写 函数名 还有一个写法 '函数名()'
        // 4. 页面中可能有很多的定时器，我们经常给定时器加标识符 （名字)
        // setTimeout(function() {
        //     console.log('时间到了');

        // }, 2000);
        function callback() {
            console.log('爆炸了');

        }
        var timer1 = setTimeout(callback, 3000);
        var timer2 = setTimeout(callback, 5000);
        // setTimeout('callback()', 3000); // 我们不提倡这个写法
```

###### 清除setTimeout定时器

<img src="assets\image-20210720091016390.png" alt="image-20210720091016390" style="zoom:67%;" />	

###### setIntetval()

```js
// 1. setInterval 
// 语法规范：  window.setInterval(调用函数, 延时时间);
setInterval(function() {
	console.log('继续输出');

}, 1000);
// 2. setTimeout  延时时间到了，就去调用这个回调函数，只调用一次 就结束了这个定时器
// 3. setInterval  每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用这个函数
```

###### 案例：倒计时效果

```html
<script>
    // 1. 获取元素 
    var hour = document.querySelector('.hour'); // 小时的黑色盒子
    var minute = document.querySelector('.minute'); // 分钟的黑色盒子
    var second = document.querySelector('.second'); // 秒数的黑色盒子
    var inputTime = +new Date('2021-7-20 18:00:00'); // 返回的是用户输入时间总的毫秒数
    countDown(); // 我们先调用一次这个函数，防止第一次刷新页面有空白 
    // 2. 开启定时器x
    setInterval(countDown, 1000);

    function countDown() {
        var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
        var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
        var h = parseInt(times / 60 / 60 % 24); //时
        h = h < 10 ? '0' + h : h;
        hour.innerHTML = h; // 把剩余的小时给 小时黑色盒子
        var m = parseInt(times / 60 % 60); // 分
        m = m < 10 ? '0' + m : m;
        minute.innerHTML = m;
        var s = parseInt(times % 60); // 当前的秒
        s = s < 10 ? '0' + s : s;
        second.innerHTML = s;
    }
```

###### 清除setInterval定时器

<img src="assets\image-20210720092745290.png" alt="image-20210720092745290" style="zoom:67%;" />	

```html
<button class="begin">开启定时器</button>
	<button class="stop">停止定时器</button>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 全局变量  null是一个空对象
        begin.addEventListener('click', function() {
            timer = setInterval(function() {
                console.log('ni hao ma');

            }, 1000);
        })
        stop.addEventListener('click', function() {
            clearInterval(timer);
        })
    </script>
```

###### 案例：发送手机短信验证码

```html
手机号码： <input type="number"> <button>发送</button>
    <script>
        // 按钮点击之后，会禁用 disabled 为true 
        // 同时按钮里面的内容会变化， 注意 button 里面的内容通过 innerHTML修改
        // 里面秒数是有变化的，因此需要用到定时器
        // 定义一个变量，在定时器里面，不断递减
        // 如果变量为0 说明到了时间，我们需要停止定时器，并且复原按钮初始状态
        var btn = document.querySelector('button');
        var time = 3; // 定义剩下的秒数
        btn.addEventListener('click', function() {
            btn.disabled = true;
            var timer = setInterval(function() {
                if (time == 0) {
                    // 清除定时器和复原按钮
                    clearInterval(timer);
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                } else {
                    btn.innerHTML = '还剩下' + time + '秒';
                    time--;
                }
            }, 1000);

        })
    </script>
```

###### this指向问题

```html
<script>
        // this 指向问题 一般情况下this的最终指向的是那个调用它的对象

        // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
        console.log(this);

        function fn() {
            console.log(this);

        }
        window.fn();
        window.setTimeout(function() {
            console.log(this);

        }, 1000);
        // 2. 方法调用中谁调用this指向谁
        var o = {
            sayHi: function() {
                console.log(this); // this指向的是 o 这个对象

            }
        }
        o.sayHi();
        var btn = document.querySelector('button');
        // btn.onclick = function() {
        //     console.log(this); // this指向的是btn这个按钮对象

        // }
        btn.addEventListener('click', function() {
                console.log(this); // this指向的是btn这个按钮对象

            })
            // 3. 构造函数中this指向构造函数的实例
        function Fun() {
            console.log(this); // this 指向的是fun 实例对象

        }
        var fun = new Fun();
    </script>
```

##### JS执行机制

###### JS是单线程

JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。

这是因为Javascript这门脚本语言诞生的使命所致——JavaScript是为处理页面中用户的交互，以及操作DOM而诞生的

比如我们对某个DOM元素进行添加和删除操作，不能同时进行。应该先进行添加，之后再删除。

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。

这样所导致的问题是∶如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

###### 同步和异步

为了解决这个问题，利用多核CPU的计算能力，HTMLS提出 Web Worker标准，允许JavaScript脚本创建多个线程。于是，JS中出现了同步和异步。

同步任务

同步任务都在主线程上执行，形成一个执行栈。

异步任务

JS的异步是通过回调函数实现的。一般而言，异步任务有以下三种类型:

1、普通事件，如click、resize等

2、资源加载，如load、error等

3、定时器，包括setInterval、setTimeout等

异步任务相关回调函数添加到任务队列中(任务队列也称为消息队列)。

###### 执行机制

1.先执行执行栈中的同步任务。
⒉.异步任务（回调函数)放入任务队列中。
3.一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

###### 事件循环

![image-20210720100105916](assets\image-20210720100105916.png)

##### location对象

###### 什么是location 对象

window对象给我们提供了一个location属性用于获取或设置窗体的URL，并且可以用于解析URL。因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象。

###### URL

统一资源定位符(Uniform Resource Locator, URL)是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。

<img src="assets\image-20210720100537080.png" alt="image-20210720100537080" style="zoom:67%;" />	

###### location对象属性

<img src="assets\image-20210720100613066.png" alt="image-20210720100613066" style="zoom:50%;" />	

重点：href   search

###### 案例：5秒后自动跳转页面

```html
<button>点击</button>
    <div></div>
    <script>
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.addEventListener('click', function() {
            // console.log(location.href);
            location.href = 'http://www.itcast.cn';
        })
        var timer = 5;
        setInterval(function() {
            if (timer == 0) {
                location.href = 'http://www.itcast.cn';
            } else {
                div.innerHTML = '您将在' + timer + '秒钟之后跳转到首页';
                timer--;
            }

        }, 1000);
    </script>
```

###### 案例：获取URL参数

login.html

```html
<form action="index.html">
        用户名： <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>
```

index.html

```html
<div></div>
    <script>
        console.log(location.search); // ?uname=andy
        // 1.先去掉？  substr('起始的位置'，截取几个字符);
        var params = location.search.substr(1); // uname=andy
        console.log(params);
        // 2. 利用=把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "ANDY"]
        var div = document.querySelector('div');
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
    </script>
```

location常用方法

![image-20210720103431276](assets\image-20210720103431276.png)	

```html
<button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // 记录浏览历史，所以可以实现后退功能
            // location.assign('http://www.itcast.cn');
            // 不记录浏览历史，所以不可以实现后退功能
            // location.replace('http://www.itcast.cn');
            location.reload(true);
        })
    </script>
```

##### navigator对象

navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值。
下面前端代码可以判断用户那个终端打开页面，实现跳转

```html
<script>   if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
	window.location.href = "../H5/index.html"; //手机
}
</script>
```

##### history对象

![image-20210720104337871](assets\image-20210720104337871.png)	



#### PC特效

##### 元素偏移量offset

###### 概述

<img src="assets\image-20210720105019886.png" alt="image-20210720105019886" style="zoom:50%;" />	

###### 常见属性

<img src="assets\image-20210720105039746.png" alt="image-20210720105039746" style="zoom:50%;" />	

```html
<div class="father">
        <div class="son"></div>
    </div>
    <div class="w"></div>
    <script>
        // offset 系列
        var father = document.querySelector('.father');
        var son = document.querySelector('.son');
        // 1.可以得到元素的偏移 位置 返回的不带单位的数值  
        console.log(father.offsetTop);
        console.log(father.offsetLeft);
        // 它以带有定位的父亲为准  如果么有父亲或者父亲没有定位 则以 body 为准
        console.log(son.offsetLeft);
        var w = document.querySelector('.w');
        // 2.可以得到元素的大小 宽度和高度 是包含padding + border + width 
        console.log(w.offsetWidth);
        console.log(w.offsetHeight);
        // 3. 返回带有定位的父亲 否则返回的是body
        console.log(son.offsetParent); // 返回带有定位的父亲 否则返回的是body
        console.log(son.parentNode); // 返回父亲 是最近一级的父亲 亲爸爸 不管父亲有没有定位
    </script>
```

###### offset与style的区别

![image-20210720113759808](assets\image-20210720113759808.png)

######  案例：获得鼠标在盒子内部的坐标

```html
<div class="box"></div>
    <script>
        // 我们在盒子内点击， 想要得到鼠标距离盒子左右的距离。
        // 首先得到鼠标在页面中的坐标（ e.pageX, e.pageY）
        // 其次得到盒子在页面中的距离(box.offsetLeft, box.offsetTop)
        // 用鼠标距离页面的坐标减去盒子在页面中的距离， 得到 鼠标在盒子内的坐标
        var box = document.querySelector('.box');
        box.addEventListener('mousemove', function(e) {
            // console.log(e.pageX);
            // console.log(e.pageY);
            // console.log(box.offsetLeft);
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            this.innerHTML = 'x坐标是' + x + ' y坐标是' + y;
        })
    </script>
```

###### 案例：拖动模态框

```js
// 4. 开始拖拽
            // (1) 当我们鼠标按下， 就获得鼠标在盒子内的坐标
        title.addEventListener('mousedown', function(e) {
            var x = e.pageX - login.offsetLeft;
            var y = e.pageY - login.offsetTop;
            // (2) 鼠标移动的时候，把鼠标在页面中的坐标，减去 鼠标在盒子内的坐标就是模态框的left和top值
            document.addEventListener('mousemove', move)

            function move(e) {
                login.style.left = e.pageX - x + 'px';
                login.style.top = e.pageY - y + 'px';
            }
            // (3) 鼠标弹起，就让鼠标移动事件移除
            document.addEventListener('mouseup', function() {
                document.removeEventListener('mousemove', move);
            })
        })
```

###### 案例：商品放大镜效果

```js
window.addEventListener('load', function() {
    var preview_img = document.querySelector('.preview_img');
    var mask = document.querySelector('.mask');
    var big = document.querySelector('.big');
    // 1. 当我们鼠标经过 preview_img 就显示和隐藏 mask 遮挡层 和 big 大盒子
    preview_img.addEventListener('mouseover', function() {
        mask.style.display = 'block';
        big.style.display = 'block';
    })
    preview_img.addEventListener('mouseout', function() {
            mask.style.display = 'none';
            big.style.display = 'none';
        })
        // 2. 鼠标移动的时候，让黄色的盒子跟着鼠标来走
    preview_img.addEventListener('mousemove', function(e) {
        // (1). 先计算出鼠标在盒子内的坐标
        var x = e.pageX - this.offsetLeft;
        var y = e.pageY - this.offsetTop;
        // console.log(x, y);
        // (2) 减去盒子高度 300的一半 是 150 就是我们mask 的最终 left 和top值了
        // (3) 我们mask 移动的距离
        var maskX = x - mask.offsetWidth / 2;
        var maskY = y - mask.offsetHeight / 2;
        // (4) 如果x 坐标小于了0 就让他停在0 的位置
        // 遮挡层的最大移动距离
        var maskMax = preview_img.offsetWidth - mask.offsetWidth;
        if (maskX <= 0) {
            maskX = 0;
        } else if (maskX >= maskMax) {
            maskX = maskMax;
        }
        if (maskY <= 0) {
            maskY = 0;
        } else if (maskY >= maskMax) {
            maskY = maskMax;
        }
        mask.style.left = maskX + 'px';
        mask.style.top = maskY + 'px';
        // 3. 大图片的移动距离 = 遮挡层移动距离 * 大图片最大移动距离 / 遮挡层的最大移动距离
        // 大图
        var bigIMg = document.querySelector('.bigImg');
        // 大图片最大移动距离
        var bigMax = bigIMg.offsetWidth - big.offsetWidth;
        // 大图片的移动距离 X Y
        var bigX = maskX * bigMax / maskMax;
        var bigY = maskY * bigMax / maskMax;
        bigIMg.style.left = -bigX + 'px';
        bigIMg.style.top = -bigY + 'px';

    })

})
```





##### 元素可视区client

###### 常见属性

![image-20210720161407078](assets\image-20210720161407078.png)

###### 立即执行函数

```js
// 1.立即执行函数: 不需要调用，立马能够自己执行的函数
        function fn() {
            console.log(1);

        }
        fn();
        // 2. 写法 也可以传递参数进来
        // 1.(function() {})()    或者  2. (function(){}());
        (function(a, b) {
            console.log(a + b);
            var num = 10;
        })(1, 2); // 第二个小括号可以看做是调用函数
        (function sum(a, b) {
            console.log(a + b);
            var num = 10; // 局部变量
        }(2, 3));
        // 3. 立即执行函数最大的作用就是 独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况
```

###### 案例：flexible.js分析

```js
(function flexible(window, document) {
    // 获取的html 的根元素
    var docEl = document.documentElement
        // dpr 物理像素比
    var dpr = window.devicePixelRatio || 1

    // adjust body font size  设置我们body 的字体大小
    function setBodyFontSize() {
        // 如果页面中有body 这个元素 就设置body的字体大小
        if (document.body) {
            document.body.style.fontSize = (12 * dpr) + 'px'
        } else {
            // 如果页面中没有body 这个元素，则等着 我们页面主要的DOM元素加载完毕再去设置body
            // 的字体大小
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
    setBodyFontSize();

    // set 1rem = viewWidth / 10    设置我们html 元素的文字大小
    function setRemUnit() {
        var rem = docEl.clientWidth / 10
        docEl.style.fontSize = rem + 'px'
    }

    setRemUnit()

    // reset rem unit on page resize  当我们页面尺寸大小发生变化的时候，要重新设置下rem 的大小
    window.addEventListener('resize', setRemUnit)
        // pageshow 是我们重新加载页面触发的事件
    window.addEventListener('pageshow', function(e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem 的大小
        if (e.persisted) {
            setRemUnit()
        }
    })

    // detect 0.5px supports  有些移动端的浏览器不支持0.5像素的写法
    if (dpr >= 2) {
        var fakeBody = document.createElement('body')
        var testElement = document.createElement('div')
        testElement.style.border = '.5px solid transparent'
        fakeBody.appendChild(testElement)
        docEl.appendChild(fakeBody)
        if (testElement.offsetHeight === 1) {
            docEl.classList.add('hairlines')
        }
        docEl.removeChild(fakeBody)
    }
}(window, document))
```



##### 元素滚动scroll

![image-20210720184354669](assets\image-20210720184354669.png)	

###### 案例：仿淘宝固定右侧侧边栏

```js
//1. 获取元素
        var sliderbar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        // banner.offestTop 就是被卷去头部的大小 一定要写到滚动的外面
        var bannerTop = banner.offsetTop
            // 当我们侧边栏固定定位之后应该变化的数值
        var sliderbarTop = sliderbar.offsetTop - bannerTop;
        // 获取main 主体元素
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');
        var mainTop = main.offsetTop;
        // 2. 页面滚动事件 scroll
        document.addEventListener('scroll', function() {
            // console.log(11);
            // window.pageYOffset 页面被卷去的头部
            // console.log(window.pageYOffset);
            // 3 .当我们页面被卷去的头部大于等于了 172 此时 侧边栏就要改为固定定位
            if (window.pageYOffset >= bannerTop) {
                sliderbar.style.position = 'fixed';
                sliderbar.style.top = sliderbarTop + 'px';
            } else {
                sliderbar.style.position = 'absolute';
                sliderbar.style.top = '300px';
            }
            // 4. 当我们页面滚动到main盒子，就显示 goback模块
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }

        })
```

##### 补充

###### 三大系列比较

![image-20210720190424068](assets\image-20210720190424068.png)

![image-20210720190625233](assets\image-20210720190625233.png)	

###### mouseenter与mouseout

![image-20210720191446565](assets\image-20210720191446565.png)



##### 动画函数封装

###### 动画原理

<img src="assets\image-20210720192220932.png" alt="image-20210720192220932" style="zoom:80%;" />	

###### 简单动画函数封装

```js
// 简单动画函数封装obj目标对象 target 目标位置
        function animate(obj, target) {
            var timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30);
        }

        var div = document.querySelector('div');
        var span = document.querySelector('span');
        // 调用函数
        animate(div, 300);
        animate(span, 200);
```

###### 给不同对象添加不同定时器

```js
<button>点击夏雨荷才走</button>
    <div></div>
    <span>夏雨荷</span>
    <script>
        // var obj = {};
        // obj.name = 'andy';
        // 简单动画函数封装obj目标对象 target 目标位置
        // 给不同的元素指定了不同的定时器
        function animate(obj, target) {
            // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案就是 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30);
        }

        var div = document.querySelector('div');
        var span = document.querySelector('span');
        var btn = document.querySelector('button');
        // 调用函数
        animate(div, 300);
        btn.addEventListener('click', function() {
            animate(span, 200);
        })
```

###### 缓动动画原理

<img src="assets\image-20210720194352574.png" alt="image-20210720194352574" style="zoom:80%;" />	

###### 缓动代码实现

多个目标值之间移动

添加回调函数

```js
<button class="btn500">点击夏雨荷到500</button>
    <button class="btn800">点击夏雨荷到800</button>
    <span>夏雨荷</span>
    <script>
        // 缓动动画函数封装obj目标对象 target 目标位置
        // 思路：
        // 1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
        // 2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长
        // 3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
        function animate(obj, target, callback) {
            // console.log(callback);  callback = function() {}  调用的时候 callback()

            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                // 步长值写到定时器的里面
                // 把我们步长值改为整数 不要出现小数的问题
                // var step = Math.ceil((target - obj.offsetLeft) / 10);
                var step = (target - obj.offsetLeft) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    if (callback) {
                        // 调用函数
                        callback();
                    }
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                obj.style.left = obj.offsetLeft + step + 'px';

            }, 15);
        }
        var span = document.querySelector('span');
        var btn500 = document.querySelector('.btn500');
        var btn800 = document.querySelector('.btn800');

        btn500.addEventListener('click', function() {
            // 调用函数
            animate(span, 500);
        })
        btn800.addEventListener('click', function() {
                // 调用函数
                animate(span, 800, function() {
                    // alert('你好吗');
                    span.style.backgroundColor = 'red';
                });
            })
            // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
            // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
```

将上述动画封装为animate.js  ,然后引用上述动画

```js
// 1. 获取元素
        var sliderbar = document.querySelector('.sliderbar');
        var con = document.querySelector('.con');
        // 当我们鼠标经过 sliderbar 就会让 con这个盒子滑动到左侧
        // 当我们鼠标离开 sliderbar 就会让 con这个盒子滑动到右侧
        sliderbar.addEventListener('mouseenter', function() {
            // animate(obj, target, callback);
            animate(con, -160, function() {
                // 当我们动画执行完毕，就把 ← 改为 →
                sliderbar.children[0].innerHTML = '→';
            });

        })
        sliderbar.addEventListener('mouseleave', function() {
            // animate(obj, target, callback);
            animate(con, 0, function() {
                sliderbar.children[0].innerHTML = '←';
            });

        })
```



##### 常见网页特效案例：网页轮播图

###### **结构搭建：**

```html
<link rel="stylesheet" href="css/index.css">
    <script src="js/animate.js"></script>
    <script src="js/index.js"></script>
```

```html
<!-- 轮播图 -->
    <div class="focus">
        <!-- 两侧按钮 -->
        <a href="javascript:;" class="glyphicon glyphicon-menu-left arrow-l"></a>
        <a href="javascript:;" class="glyphicon glyphicon-menu-right arrow-r"></a>
        <!-- 轮播图片 -->
        <ul class="pic">
            <li><a href="#"><img src="img/源计划.jpg" alt=""></a></li>
            <li><a href="#"><img src="img/西部牛仔.jpg" alt=""></a></li>
            <li><a href="#"><img src="img/灵魂莲华.jpg" alt=""></a></li>
            <li><a href="#"><img src="img/真实伤害.jpg" alt=""></a></li>
        </ul>
        <!-- 小圆圈 -->
        <ul class="circle">
        </ul>
    </div>
```

```js
function animate(obj, target, callback) {
    //清除之前的定时器
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
        // 划分步长
        var step = (target - obj.offsetLeft) / 10;
        // 步长取整
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            clearInterval(obj.timer);
            // 回调函数
            callback && callback();
        }
        // 设置距离
        obj.style.left = obj.offsetLeft + step + 'px';
    }, 15);
}

```

###### **鼠标经过显示隐藏左右按钮**

```js
var focus = document.querySelector('.focus');
// 显示隐藏左右按钮
    focus.addEventListener('mouseenter', function () {
        arrow_l.style.display = 'block';
        arrow_r.style.display = 'block';
        //clearInterval(timer);
    });
    focus.addEventListener('mouseleave', function () {
        arrow_l.style.display = 'none';
        arrow_r.style.display = 'none';
        //timer = setInterval(function () {
        //    arrow_r.click();
        //}, 2000);
    });
```

​			需要先在css中给 `display： none；`

###### **动态生成小圆圈**

```js
// 动态添加小圆圈
    var pic = document.querySelector('.pic');
    var circle = document.querySelector('.circle');
    for (var i = 0; i < pic.children.length; i++) {
        // 给circle创建li
        var li = document.createElement('li');
        // 给li设置index属性
        //li.setAttribute('index', i);
        // 把li放入circle中
        circle.appendChild(li);
    }
```

###### **小圆圈排他思想**

```js
//点击小圆圈 排他变白
        li.addEventListener('click', function () {
            for (var i = 0; i < circle.children.length; i++) {
                circle.children[i].className = '';
            }
            this.className = 'current';
```

###### **点击小圆圈滚动图片**

```js
// 动态添加小圆圈
    var pic = document.querySelector('.pic');
    var circle = document.querySelector('.circle');
    for (var i = 0; i < pic.children.length; i++) {
        // 给circle创建li
        var li = document.createElement('li');
        // 给li设置index属性
        li.setAttribute('index', i);
        // 把li放入circle中
        circle.appendChild(li);
        //点击小圆圈 排他变白
        li.addEventListener('click', function () {
            for (var i = 0; i < circle.children.length; i++) {
                circle.children[i].className = '';
            }
            this.className = 'current';
            // 拿到索引号
            var index = this.getAttribute('index');
            // 把索引号给num_btn,num_circle
            num_btn = index;
            num_circle = index
            // 拿到单个盒子宽度
            var focusWidth = focus.offsetWidth;
            // 使用动画animate移动图片
            // console.log(focusWidth);
            // console.log(index);
            animate(pic, -index * focusWidth);
        })
    }
```

###### **右键按钮无缝滚动**

```js
// 左右按钮切换图片
    // 按钮变量  0 1 2 3
    var num_btn = 0;
    // 小圆圈变量 0 1 2 3
   // var num_circle = 0;

    // 右侧按钮
    arrow_r.addEventListener('click', function () {
        // console.log(pic.children.length);
        if (num_btn == pic.children.length - 1) {
            pic.style.left = 0;
            num_btn = 0;
        }
        num_btn++;
        animate(pic, -num_btn * focusWidth);
        //小圆圈切换
        num_circle++;
        // 从最后一个圈到第一个
        if (num_circle == circle.children.length) {
            num_circle = 0;
        }
        circleChange();
    })
```

###### **克隆第一张图片**

```js
// 把circle里面的第一个小li设置类名为 current
    circle.children[0].className = 'current';
    // 克隆第一张图片(li)放到ul 最后面
    var first = pic.children[0].cloneNode(true);
    pic.appendChild(first);
```

###### **小圆圈跟随右侧按钮变化**

```js
    // 封装小圆圈排他函数
    function circleChange() {
        for (var i = 0; i < circle.children.length; i++) {
            circle.children[i].className = '';
        }
        circle.children[num_circle].className = 'current';
    }
```

```js
//小圆圈切换
        num_circle++;
        // 从最后一个圈到第一个
        if (num_circle == circle.children.length) {
            num_circle = 0;
        }
        circleChange();
```

###### **两个小bug**

​	图片显示不符合预期

​	小圆圈显示不符合预期

```js
            num_btn = index;
            num_circle = index
```

###### **左侧按钮**

```js
    // 左侧按钮
    arrow_l.addEventListener('click', function () {
        // console.log(pic.children.length);
        if (num_btn == 0) {
            num_btn = pic.children.length - 1;
            pic.style.left = -num_btn * focusWidth + 'px';

        }
        num_btn--; //-1 -2 -3 -4
        //4 3 2 1
        // 打印num_btn
        // console.log("num_btn:" + num_btn);
        animate(pic, -num_btn * focusWidth);
        //小圆圈切换
        num_circle--;//-1 -2 -3 
        //3 2 1   
        // 从最后一个圈到第一个
        if (num_circle < 0) {
            num_circle = circle.children.length - 1;
        }
        num_circle = num_circle < 0 ? circle.children.length - 1 : num_circle;
        // 打印num_circle
        // console.log('num_circle:' + num_circle);
        circleChange();
    })
```

###### **自动播放**

```js
    // 自动播放（模拟手动点击右键）
    var timer = setInterval(function () {
        arrow_r.click();
    }, 2000);
```

```js
    focus.addEventListener('mouseenter', function () {
        arrow_l.style.display = 'block';
        arrow_r.style.display = 'block';
        clearInterval(timer);
    });
    focus.addEventListener('mouseleave', function () {
        arrow_l.style.display = 'none';
        arrow_r.style.display = 'none';
        timer = setInterval(function () {
            arrow_r.click();
        }, 2000);
    });
```

##### 节流阀

![image-20210721141835702](assets\image-20210721141835702.png)	

##### 返回顶部效果

使用缓动动画

```js
    // 3. 当我们点击了返回顶部模块，就让窗口滚动的页面的最上方
        goBack.addEventListener('click', function() {
            // 里面的x和y 不跟单位的 直接写数字即可
            // window.scroll(0, 0);
            // 因为是窗口滚动 所以对象是window
            animate(window, 0);
        });
```

动画

```js
// 动画函数
        function animate(obj, target, callback) {
            // console.log(callback);  callback = function() {}  调用的时候 callback()

            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                // 步长值写到定时器的里面
                // 把我们步长值改为整数 不要出现小数的问题
                // var step = Math.ceil((target - obj.offsetLeft) / 10);
                var step = (target - window.pageYOffset) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (window.pageYOffset == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    // if (callback) {
                    //     // 调用函数
                    //     callback();
                    // }
                    callback && callback();
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                // obj.style.left = window.pageYOffset + step + 'px';
                window.scroll(0, window.pageYOffset + step);
            }, 15);
        }
```



##### 筋斗云案例

结构

```html
<div id="c_nav" class="c-nav">
        <span class="cloud"></span>
        <ul>
            <li class="current"><a href="#">首页新闻</a></li>
            <li><a href="#">师资力量</a></li>
            <li><a href="#">活动策划</a></li>
            <li><a href="#">企业文化</a></li>
            <li><a href="#">招聘信息</a></li>
            <li><a href="#">公司简介</a></li>
            <li><a href="#">我是佩奇</a></li>
            <li><a href="#">啥是佩奇</a></li>
        </ul>
    </div>
```

给所有li绑定事件

```js
window.addEventListener('load', function() {
            // 1. 获取元素
            var cloud = document.querySelector('.cloud');
            var c_nav = document.querySelector('.c-nav');
            var lis = c_nav.querySelectorAll('li');
            // 2. 给所有的小li绑定事件 
            // 这个current 做为筋斗云的起始位置
            var current = 0;
            for (var i = 0; i < lis.length; i++) {
                // (1) 鼠标经过把当前小li 的位置做为目标值
                lis[i].addEventListener('mouseenter', function() {
                    animate(cloud, this.offsetLeft);
                });
                // (2) 鼠标离开就回到起始的位置 
                lis[i].addEventListener('mouseleave', function() {
                    animate(cloud, current);
                });
                // (3) 当我们鼠标点击，就把当前位置做为目标值
                lis[i].addEventListener('click', function() {
                    current = this.offsetLeft;
                });
            }
        })

```



#### 移动端网页特效

##### 触屏事件

![image-20210721144717686](assets\image-20210721144717686.png)	

##### 触屏事件对象

![image-20210721144843645](assets\image-20210721144843645.png)	

```js
// 触摸事件对象
        // 1. 获取元素
        // 2. 手指触摸DOM元素事件
        var div = document.querySelector('div');
        div.addEventListener('touchstart', function (e) {
            // console.log(e);
            // touches 正在触摸屏幕的所有手指的列表 
            // targetTouches 正在触摸当前DOM元素的手指列表
            // 如果侦听的是一个DOM元素，他们两个是一样的
            // changedTouches 手指状态发生了改变的列表 从无到有 或者 从有到无
            // 因为我们一般都是触摸元素 所以最经常使用的是 targetTouches
            console.log(e.targetTouches[0]);
            // targetTouches[0] 就可以得到正在触摸dom元素的第一个手指的相关信息比如 手指的坐标等等


        });
        // 3. 手指在DOM元素身上移动事件
        div.addEventListener('touchmove', function () {


        });
        // 4. 手指离开DOM元素事件
        div.addEventListener('touchend', function (e) {
            // console.log(e);
            // 当我们手指离开屏幕的时候，就没有了 touches 和 targetTouches 列表
            // 但是会有 changedTouches


        });
```

##### 移动端拖动元素

```js
// （1） 触摸元素 touchstart：  获取手指初始坐标，同时获得盒子原来的位置
        // （2） 移动手指 touchmove：  计算手指的滑动距离，并且移动盒子
        // （3） 离开手指 touchend:
        var div = document.querySelector('div');
        var startX = 0; //获取手指初始坐标
        var startY = 0;
        var x = 0; //获得盒子原来的位置
        var y = 0;
        div.addEventListener('touchstart', function(e) {
            //  获取手指初始坐标
            startX = e.targetTouches[0].pageX;
            startY = e.targetTouches[0].pageY;
            x = this.offsetLeft;
            y = this.offsetTop;
        });

        div.addEventListener('touchmove', function(e) {
            //  计算手指的移动距离： 手指移动之后的坐标减去手指初始的坐标
            var moveX = e.targetTouches[0].pageX - startX;
            var moveY = e.targetTouches[0].pageY - startY;
            // 移动我们的盒子 盒子原来的位置 + 手指移动的距离
            this.style.left = x + moveX + 'px';
            this.style.top = y + moveY + 'px';
            e.preventDefault(); // 阻止屏幕滚动的默认行为
        });
```

##### swiper插件的使用

###### 引入相关文件

```html
<!-- 引入swipercss文件 -->
    <link rel="stylesheet" href="css/swiper.min.css">
    <!-- 引入swiper js 文件 -->
    <script src="js/swiper.min.js"></script>
    <!-- 引入我们自己的js文件 -->
    <script src="js/index.js"></script>
    <title>Document</title>
```

###### 按照规定语法使用

复制主体结构放入html中

css结构放入css中

js放入js中

##### 其他移动端常见插件

superslide : http://www.superslide2.com/

iscroll : https://github.com/cubiq/iscroll

视频插件zy.media.js

https://www.cnblogs.com/fuyunlin/p/14479629.html



#### 本地存储

##### sessionStorage

![image-20210721155009374](assets\image-20210721155009374.png)

```html
<input type="text">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空所有数据</button>
    <script>
        console.log(localStorage.getItem('username'));

        var ipt = document.querySelector('input');
        var set = document.querySelector('.set');
        var get = document.querySelector('.get');
        var remove = document.querySelector('.remove');
        var del = document.querySelector('.del');
        set.addEventListener('click', function() {
            // 当我们点击了之后，就可以把表单里面的值存储起来
            var val = ipt.value;
            sessionStorage.setItem('uname', val);
            sessionStorage.setItem('pwd', val);
        });
        get.addEventListener('click', function() {
            // 当我们点击了之后，就可以把表单里面的值获取过来
            console.log(sessionStorage.getItem('uname'));

        });
        remove.addEventListener('click', function() {
            // 
            sessionStorage.removeItem('uname');

        });
        del.addEventListener('click', function() {
            // 当我们点击了之后，清除所有的
            sessionStorage.clear();

        });
    </script>
```



##### localStorage

![image-20210721155044617](assets\image-20210721155044617.png)

```html
    <input type="text">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空所有数据</button>
    <script>
        var ipt = document.querySelector('input');
        var set = document.querySelector('.set');
        var get = document.querySelector('.get');
        var remove = document.querySelector('.remove');
        var del = document.querySelector('.del');
        set.addEventListener('click', function() {
            var val = ipt.value;
            localStorage.setItem('username', val);
        })
        get.addEventListener('click', function() {
            console.log(localStorage.getItem('username'));

        })
        remove.addEventListener('click', function() {
            localStorage.removeItem('username');

        })
        del.addEventListener('click', function() {
            localStorage.clear();

        })
    </script>
```





#### jQuery

##### 	

