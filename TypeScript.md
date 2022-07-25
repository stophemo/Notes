# TypeScript

### 简介

`TypeScript`是`JavaScript`的`超集`

TS 与 JS 的关系 如同 Less/Sass 与 css的关系

就像Less/Sass是对CSS进行扩展一样, TS也是对JS进行扩展

就像Less/Sass最终会转换成CSS一样, 我们编写好的TS代码最终也会换成JS

### 为什么需要TypeScript？

`JavaScript`是`弱类型`, 很多错误只有在运行时才会被发现

`TypeScript`提供了一套`静态检测机制`, 可以帮助我们在编译时就发现错误

#### 运行时 

所谓运行时就是代码跑起来了,被装载到`内存`中去了

#### 编译时

`编译`，就是编译器帮你把源代码翻译成机器能识别的代码，这时的错误就叫编译时错误,这个过程中做的啥类型检查也就叫编译时类型检查,或`静态类型检查`(所谓静态嘛就是没把真把代码放内存中运行起来,而只是把代码当作文本来扫描下)

### TypeScript特点

- 支持最新的JavaScript新特特性
- 支持代码静态检查
- 支持诸如C,C++,Java,Go等后端语言中的特性 (枚举、泛型、类型转换、命名空间、声明文件、类、接口等)

### 搭建环境

#### 安装最新版typescript

```git
npm i -g typescript
```

#### 安装ts-node

```
npm i -g ts-node
```

#### 创建一个 tsconfig.json 文件

```
tsc --init
```

**然后新建index.ts,输入相关练习代码，然后执行 `ts-node index.ts`**

**官方也提供了一个在线开发 TypeScript 的云环境——[Playground](https://link.juejin.cn/?target=https%3A%2F%2Fwww.typescriptlang.org%2Fzh%2Fplay)。**



### 基本数据类型

```tsx
//JS 原始数据类型
let str: string = "jack";
let num: number = 24;
let bool: boolean = false;
let u: undefined = undefined;
let n: null = null;
let big: bigint = 100n;
let sym: symbol = Symbol("me"); 
// JS 引用数据类型
let obj: object = {x: 1};
```

#### Tips：

默认情况下 `null` 和 `undefined` 是所有类型的子类型。 就是说你可以把 `null` 和 `undefined` 赋值给其他类型。

严格模式下 `"strictNullChecks":true` ，`null` 和 `undefined` 只能赋值给 `void` 和它们各自的类型。

类型不兼容 ts(2322)错误



### 其他类型



#### Array

##### 定义方式

```ts
let arr: string[] = ['1', '2'];
let arr2: Array<string> = ['1', '2'];
```

##### 定义联合类型数组

```tsx
let arr:(number | string)[];
// 表示定义了一个名称叫做arr的数组, 
// 这个数组中将来既可以存储数值类型的数据, 也可以存储字符串类型的数据
arr3 = [1, 'b', 2, 'c'];
```

##### 定义对象数组

```tsx
interface Arrobj { 
  name: string,
  age: number
}
let arr4: Arrobj[] = [{ name: 'jack', age: 22 }];
```



#### 函数

##### 函数声明

```tsx
function sum(x: number, y: number): number {
    return x + y;
}
```

##### 函数表达式

`完整写法`

```tsx
//(x: number, y: number) => number 表示当前这个函数的类型
// function (x: number, y: number): number {return x + y;};  就相当于符合上面条件的返回值
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

##### 用接口定义函数**类型**

```tsx
interface SearchFunc{
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string,subString:string){
     return source.search(subString) !== -1  
}
```

##### 可选参数

```tsx
function sum(x: number, y: number, z?:number): number {
    return x + y;
}
```

**注意点：可选参数后面不允许再出现必需参数**

##### 参数默认值

```tsx
function sum(x: number, y: number, z:number=3): number {
    return x + y + z;
}
```

##### 剩余参数

```ts
function push(array: any[], ...items: any[]) {
    items.forEach(function(item) {
        array.push(item);
    });
}
let a = [];
push(a, 1, 2, 3);
```

##### 函数重载

```ts
function add(x, y) {
 return x + y;
}
add(1, 2); // 3
add("1", "2"); //"12"
```

TypeScript 编译器开启 `noImplicitAny` 的配置项时 ,以上代码会提示以下错误信息：`Parameter 'y' implicitly has an 'any' type`  该信息告诉我们参数 x 和参数 y 隐式具有 `any` 类型

修改如下：

```tsx
type Combinable = string | number

function add(a: Combinable, b: Combinable) {
  if (typeof a === 'string' || typeof b === 'string') {
   return a.toString() + b.toString();
  }
  return a + b;
}
console.log("add(1, 2)", add(1, 2),"add('1', '2')",add('1', '2'))
```

我们把结果保存到一个名为 `result` 的变量上，这时候我们想当然的认为此时 `result` 的变量的类型为 `string` 我们就可以正常调用字符串对象上的 `split` 方法

```tsx
const result = add('aaa', ' bbb')
console.log(result.split(' '));
```

这时 TypeScript 编译器又出现以下错误信息了：

```
Property 'split' does not exist on type 'string | number'.
Property 'split' does not exist on type 'number'.
```

很明显 `number` 类型的对象上并不存在 `split` 属性。问题又来了，那如何解决呢？这时我们就可以利用 TypeScript 提供的`函数重载`特性。

**函数重载或方法重载 是使用 `相同名称` 和 `不同参数数量或类型` 创建`多个方法` 的 一种能力**

```tsx
type Types = number | string
function add(a: number, b: number): number
function add(a: string, b: string): string
function add(a: string, b: number): string
function add(a: number, b: string): string
function add(a: Types, b: Types) {
  if (typeof a === 'string' || typeof b === 'string') {
    return a.toString() + b.toString()
  }
  return a + b
}
const result = add('aaa', ' bbb')
console.log(result.split(' '))
```





#### Tuple(元组)

##### 定义

众所周知，数组一般由同种类型的值组成，但有时我们需要在单个变量中存储不同类型的值，这时候我们就可以使用元组。

在 JavaScript 中是没有元组的，元组是 TypeScript 中特有的类型，其工作方式类似于数组。

元组最重要的特性是可以限制`数组元素的个数和类型`，它特别适合用来实现多值返回。

```tsx
let x: [string, number]; 
// 类型必须匹配且个数必须为2

x = ['hello', 10]; // OK 
x = ['hello', 10,10]; // Error 
x = [10, 'hello']; // Error
```

注意，元组类型只能表示一个已知元素数量和类型的数组，长度已指定，越界访问会提示错误。如果一个数组中可能有多种类型，数量和类型都不确定，那就直接`any[]`



##### 元组类型的解构赋值

```tsx
let x: [string, number] = ['hello', 10];
let [a, b] = x;
console.log(`a:${a}`);
console.log(`b:${b}`);
```

##### 元组类型的可选元素

与函数签名类型类似，在定义元组类型时，我们也可以通过 `?` 号来声明元组类型的可选元素，具体的示例如下：

```ts
type Point = [number, number?, number?];

const x: Point = [10]; // 一维坐标点
const xy: Point = [10, 20]; // 二维坐标点
const xyz: Point = [10, 20, 30]; // 三维坐标点

console.log(x.length); // 1
console.log(xy.length); // 2
console.log(xyz.length); // 3
```

##### 元组类型的剩余元素

```tsx
type RestTupleType = [number, ...string[]];
let restTuple: RestTupleType = [666, "Semlinker", "Kakuqo", "Lolo"];
console.log(restTuple);
```



##### 只读的元组类型

```tsx
const point:readonly [number,number] =  [10,20]
```

在使用 `readonly` 关键字修饰元组类型之后，任何企图修改元组中元素的操作都会抛出异常：

#### void

`void`表示没有任何类型，和其他类型是平等关系，不能直接赋值:

声明一个`void`类型的变量没有什么大用，我们一般也只有在函数没有返回值时去声明。



#### never

`never`类型表示的是那些永不存在的值的类型

值会永不存在的两种情况：

1. 如果一个函数执行时抛出了**异常**，那么这个函数永远不存在返回值（因为抛出异常会直接中断程序运行，这使得程序运行不到返回值那一步，即具有不可达的终点，也就永不存在返回了）；
2. 函数中执行无限循环的代码（**死循环**），使得程序永远无法运行到函数返回值那一步，永不存在返回。



`never`类型同`null`和`undefined`一样，也是任何类型的子类型，也可以赋值给任何类型。

但是没有类型是`never`的子类型或可以赋值给`never`类型（除了`never`本身之外），即使`any`也不可以赋值给`never`

#### any

在 TypeScript 中，任何类型都可以被归为 `any `类型。这让 any 类型成为了类型系统的顶级类型.

如果是一个普通类型，在赋值过程中改变类型是不被允许的：

```tsx
let a: string = 'seven';
a = 7;
// TS2322: Type 'number' is not assignable to type 'string'.
```

但如果是 `any` 类型，则允许被赋值为任意类型。

```tsx
let a: any = 666;
a = "Semlinker";
a = false;
a = 66
a = undefined
a = null
a = []
a = {}
```

**变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型**

```tsx
let something;
something = 'seven';
something = 7;
something.setName('Tom');
```

在许多场景下，`any`太宽松了。使用 `any` 类型，可以很容易地编写类型正确但在运行时有问题的代码。

如果我们使用 `any` 类型，就无法使用 TypeScript 提供的大量的保护机制。请记住，`any 是魔鬼！`尽量不要用any。

为了解决 `any` 带来的问题，TypeScript 3.0 引入了 `unknown` 类型。

#### unknown

`unknown`与`any`一样，所有类型都可以分配给`unknown`:



unknown 与 any的最大区别是：

任何类型的值可以赋值给`any`，同时`any`类型的值也可以赋值给任何类型。

`unknown` 任何类型的值都可以赋值给它，但它只能赋值给`unknown`和`any`



这种机制起到了很强的预防性，更安全，这就要求我们必须缩小类型，我们可以使用`typeof`、`类型断言`等方式来缩小未知范围：



```tsx
function getDogName() {
 let x: unknown;
 return x;
};
const dogName = getDogName();
// 直接使用
const upName = dogName.toLowerCase(); // Error
// typeof
if (typeof dogName === 'string') {
  const upName = dogName.toLowerCase(); // OK
}
// 类型断言 
const upName = (dogName as string).toLowerCase(); // OK

```



#### Number、String、Boolean、Symbol

首字母大写的 Number、String、Boolean、Symbol 类型,是相应原始类型的`包装对象`，姑且把它们称之为对象类型。

从`类型兼容性`上看，原始类型兼容对应的对象类型，反过来对象类型不兼容对应的原始类型。

```tsx
let num: number;
let Num: Number;
Num = num; // ok
num = Num; // ts(2322)报错
```

**不要使用对象类型来注解值的类型，因为这没有任何意义。**



#### object、Object 和 {}

小 `object` 代表的是所有非原始类型，也就是说我们不能把 number、string、boolean、symbol等 原始类型赋值给 object。在严格模式下，`null` 和 `undefined` 类型也不能赋给 object。



JavaScript 中以下类型被视为原始类型：

`string`

`boolean`

`number`

`bigint`

`symbol`

`null` 

`undefined`



大`Object` 代表所有拥有 toString、hasOwnProperty 方法的类型，所以所有原始类型、非原始类型都可以赋给 Object。同样，在严格模式下，null 和 undefined 类型也不能赋给 Object。



### 类型推断

在很多情况下，TypeScript 会根据上下文环境自动推断出变量的类型，无须我们再写明类型注解

我们把 TypeScript 这种基于赋值表达式推断类型的能力称之为`类型推断`

比如我们能根据 return 语句推断函数返回的类型

```tsx
function sum(a: number, b: number) { 
  return a + b;
}
const x = sum(3, 4);
console.log(typeof(x));
```

如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 `any` 类型而完全不被类型检查



### 类型断言

我们可以使用一种笃定的方式——**类型断言**（类似仅作用在类型层面的强制类型转换）告诉 TypeScript 按照我们的方式做类型检查。

比如，我们可以使用 as 语法做类型断言，如下代码所示：

```tsx
const arrayNumber: number[] = [1, 2, 3, 4];
const greaterThan2: number = arrayNumber.find(num => num > 2) as number;
```



#### 语法

```tsx
// 尖括号 语法
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

```tsx
// as 语法
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

以上两种方式虽然没有任何区别，但是尖括号格式会与react中JSX产生语法冲突，因此我们更推荐使用 as 语法。



#### 非空断言

在上下文中当类型检查器无法断定类型时，一个新的后缀表达式操作符 `!` 可以用于断言操作对象是非 null 和非 undefined 类型。

**具体而言，x! 将从 x 值域中排除 null 和 undefined 。**

```tsx
let mayNullOrUndefinedOrString: null | undefined | string;
mayNullOrUndefinedOrString!.toString(); // ok
mayNullOrUndefinedOrString.toString(); // ts(2531)
```



#### 确定赋值断言

```tsx
// 确定赋值断言
let x: number;
initialize();

// Variable 'x' is used before being assigned.(2454)
console.log(2 * x);

function initialize() { 
  x = 10;
}
```

很明显该异常信息是说变量 x 在赋值前被使用了，要解决该问题，我们可以使用确定赋值断言：

```tsx
// 确定赋值断言
let x!: number;
initialize();

console.log(2 * x);

function initialize() { 
  x = 10;
}
```





### 字面量类型





### 类型拓宽



### 类型缩小



### 联合类型

联合类型表示取值可以为多种类型中的一种，使用 `|` 分隔每个类型。

```tsx
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven'; // OK
myFavoriteNumber = 7; // OK
```



### 类型别名

```tsx
type Message = string | string[];
let greet = (message: Message) => {
  // ...
};
```



### 交叉类型

交叉类型是将多个类型合并为一个类型。 这让我们可以把现有的多种类型叠加到一起成为一种类型，它包含了所需的所有类型的特性，使用`&`定义交叉类型。

```tsx
{
  type Useless = string & number;
}
```

类型别名 Useless 的类型就是个 `never`



交叉类型真正的用武之地就是将多个接口类型合并成一个类型，从而实现等同接口继承的效果，也就是所谓的合并接口类型，如下代码所示：

```tsx
type IntersectionType = 
{ id: number; name: string; } & { age: number };
      const mixed: IntersectionType = {
        id: 1,
        name: 'name',
        age: 18
      }
```

在上述示例中，我们通过交叉类型，使得 IntersectionType 同时拥有了 id、name、age 所有属性，这里我们可以试着将合并接口类型理解为求并集。





### 接口

**赋值的时候，变量的形状必须和接口的形状保持一致**

```tsx
interface Person {
    name: string;
    age: number;
}
let tom: Person = {
    name: 'Tom',
    age: 22
};
```



### 泛型

```tsx
function identity<T>(arg: T): T {
  return arg;
}
```

其中 `T` 代表 **Type**，在定义泛型时通常用作第一个类型变量名称。但实际上 `T` 可以用任何有效名称代替。除了 `T` 之外，以下是常见泛型变量代表的意思：

- K（Key）：表示对象中的键类型；
- V（Value）：表示对象中的值类型；
- E（Element）：表示元素类型。



![img](assets/1729b3d9773f34adtplv-t2oaga2asx-watermark.awebp)



### 高效TS代码



#### 接口继承

```tsx
interface Person { 
  firstName: string; 
  lastName: string;
}

interface PersonWithBirthDate extends Person { 
  birth: Date;
}

```

当然除了使用 `extends` 关键字之外，也可以使用交叉运算符（&）：

```tsx
type PersonWithBirthDate = Person & { birth: Date };
```



#### 定义一个类型来匹配一个初始配置对象的「形状」

```tsx
const INIT_OPTIONS = {
  width: 640,
  height: 480,
  color: "#00FF00",
  label: "VGA",
};

interface Options {
  width: number;
  height: number;
  color: string;
  label: string;
}
```

其实，对于 Options 接口来说，你也可以使用 typeof 操作符来快速获取配置对象的「形状」：

```ts
type Options = typeof INIT_OPTIONS;
```



#### 使用更精确的类型替代字符串类型

对于 `Album` 类型，你希望 `releaseDate` 属性值的格式为 `YYYY-MM-DD`，而 `recordingType` 属性值的范围为 `live` 或 `studio`



接口定义:

`releaseDate: Date;`

`recordingType: "studio" | "live";`

```tsx
interface Album {
  artist: string; // 艺术家
  title: string; // 专辑标题
  releaseDate: Date; // 发行日期：YYYY-MM-DD
  recordingType: "studio" | "live"; // 录制类型："live" 或 "studio"
}
```

赋值

```tsx
const dangerous: Album = {
  artist: "Michael Jackson",
  title: "Dangerous",
  releaseDate: new Date("1991-11-31"),
  recordingType: "studio",
};
```

