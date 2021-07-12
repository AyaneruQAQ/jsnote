





# JS笔记

###### 1.js输出：

document.write()仅用作测试，且在文档加载完成后执行会删除所有页面内容。

###### **2**.js加法

如下`var x="2"+1+1`，结果为211；`var x=1+1+"2"`，结果为22。（字符串➕数字，返回结果为字符串）。

###### 3.字符串与数字比较

会把字符串转换为数值，空字符串将被转换为 0。非数值字符串将被转换为始终为 false 的 NaN

###### 4.jquery选择器

class选择器`$('.class')` 	id选择器`$('#id')`		标签选择器`$('button')`

###### 5.js string转int

`var i = parseInt(“20”)`

###### 6.判断一个变量是否为`NaN`

`!(test == test)`若返回结果为`true`，则test是`NaN`

###### 7.js除法强制取2位小数

```js
        function toDecimal2(x) {//除法保留2位
            var f = parseFloat(x);
            if (isNaN(f)) {
                return false;
            }
            var f = Math.round(x * 100) / 100;
            var s = f.toString();
            var rs = s.indexOf('.');
            if (rs < 0) {
                rs = s.length;
                s += '.';
            }
            while (s.length <= rs + 2) {
                s += '0';
            }
            return s;
        }
```

###### 8.DOM元素的id值是唯一的

###### 9.获取url特定name的参数值

​	location.search：**如果“#”之前没有“？”search取值为空**

```js
//没有#的路径可以使用下面的函数	
function getFrom(name){
		var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");  
		var r = location.search.substr(1).match(reg); //location.search获取？后的内容
		return r ? unescape(decodeURI(r[2])) : null ;
	}
	
```

```javascript
//通用的方法
    let r;
    let url = window.location.toString();
    let ur = url.split(/[#?=&]/);//
    for(let i = 0;i < ur.length;i++){
        if(ur[i]==='imei'){
             r = ur[i+1];
             console.log(r);
        }
    }
```

###### 10.按分钟倒计时显示，也要1秒执行一次倒计时函数！！！！

###### 11.ajax的send（），只在post请求时才需要参数

###### 12.原生js设置style

```javascript
var pay1 = document.getElementsByClassName("pay");
document.body.style.backgroundColor = "white";
document.documentElement.style.backgroundColor = "white";//设置html背景色
pay1[0].style.color = "black";
```

###### 13.react事件绑定传参

​	使用es6箭头函数

```jsx
onClick={()=>this.button_Click(参数)}
```

###### 14.url传#等特殊参数时要做转义

​	例：# => %23

###### 15.判断第一次打开页面

```js
        if(sessionStorage.getItem("firstopen")){//null
            sessionStorage.setItem("firstopen","0")
            // console.log("96"+sessionStorage.getItem("firstopen"))
        }else{
            sessionStorage.setItem("firstopen","1")
            // console.log("99"+sessionStorage.getItem("firstopen"))
        }
```

**第一次**：打开整个网站第一次，关掉页面再打开还是判断为第一次。其余情况，例如路由跳转到首页则不为第一次

###### 16.js数组深拷贝、浅拷贝

​	

```js
let b= JSON.parse(JSON.stringify(a))//使用json方法实现深拷贝

stringify() js对象转化成JSON字符串
parse() 字符串转化成对象

//es6实现数组深拷贝
let a1 = [1,2,3]
let a2 = [...a1]
//可以下面这样使用
                                   
//如果数组所有项都为非引用类型，则slice(0)可以视作深拷贝，反之则不行
```

###### 16.concat不改变原数组

```
let a = [1,2,3]
a.concat(4)
//此时a=[1,2,3],没有改变
```

​	**splice()会改变原数组**

###### 17.input框绑定键盘enter事件

```jsx
onKeyDown={
    (e) => {
            if (e.keyCode == '13') {
                   this.search();
                   console.log('enter')
            }
          }
}
```

###### 18.es6寻找符合条件的数组项下标

```
array.findIndex(这里填条件)

array.indexOf(item)//返回下标
```

###### 19.js数据类型：

​	基本数据类型：String、Number、Boolean、Null、Undefined

​	引用数据类型：Object、Array、Function

​	typeof返回的数据类型有string、number(NaN)、boolean、undefined、object（null、array）、function

###### 20.array.reduce(func,initvalue)

###### 21.全局变量

```js
let/const a = 123 //在class里直接使用
var b = 123 //在class里要通过this.b来使用
```

###### 22.数组解构按次序，对象解构按属性名

**解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象**

###### 23.for...of和foreach遍历数组，foreach不可中途跳出，而前者可以配合break、return使用

###### 24.call/apply/bind,让this指针指向传递的第一个参数，如果第一个参数为空，则指向全局变量

###### 25.js中数组成员的类型可以是不一致的

```js
let arr = [1,'1']
typeof(arr[0])//number
typeof(arr[1])//string
```

###### 26.let self = this

​	普通函数中this指向window对象

```js
function a(){
	this.name = "hello"; 
 
	function b(){  //b只是一个普通函数，不是a的属性方法
		alert(this.name);
	}
	b();  //调用b
}

new a(); //新建一个a对象，此时alert name undefined
```

```js
function a(){
	var self = this;
	this.name = "hello"; 
 
	function b(){  //b只是一个普通函数，不是a的属性方法
		alert(self.name);
	}
	b();  //调用b
}
 
new a(); //新建一个a对象，此时alert name = hello
```

```js

var param = "hello";
var myObject = {
  param: 123,
  method: function(){
    alert( this.param );  //this指向myObject，因为这个函数是对象的属性
  },
  method2: function(){
    setTimeout(function(){  //匿名函数
      alert( this.param ); //this指向windows
    },100);
  }
}
myObject.method(); //alert 123
myObject.method2();  //alert hello
```

###### 27.尽量少用全局变量，因为js内存回收机制难以判断什么时候可以回收全局变量

​	内存泄漏：创建了无法回收的对象

###### 28.js内存空间

​	栈：存基本数据类型和指向复杂数据类型的指针

​	堆：复杂数据类型（对象、数组、函数）

###### 29.lodash中有很多好用的方法

​	函数去抖debounce

​	函数节流throttle

​	[](https://blog.csdn.net/duola8789/article/details/78871789)

###### 30.Promise对象

```js
let promise = new Promise()
promise
.then(result => {···})
.catch(error => {···})//catch捕获rejection
.finally(() => {···});
```

###### 31.async/await:generator函数的语法糖

​	内置执行器，不需要next

​	返回Promise对象

​	await后面不一定要Promise对象

###### 31.Image()

​	js中缓存图片,预加载

```js
 function loadimg (){//在需要显示图片的时候执行该函数
                var tmpt = document.getElementById('cs');
                var oimg = new Image();
                oimg.onload = function(){
                    tmpt.src = oimg.src;
                }
                oimg.src = 'wx.png';
                
            }
```

###### 32.闭包：在一个函数内创建另一个函数

​	闭包可用来模拟私有方法（模块模式）

###### 33.原型链（`__proto__`指针链）

​	**prototype**（原型）是函数特有的属性

​	`__proto__`是所有对象都有的属性



​	动态继承

```js
function Engineer (name, projs, mach) {
  WorkerBee.call(this, name, "engineering", projs);//使用call/apply实现继承
  this.machine = mach || "";//mach有值返回mach，否则返回""
}
Engineer.prototype = new WorkerBee;//显式设置原型实现动态继承(属性)
```

​	动态改变继承的值

```js
function Employee () {
  this.dept = "general";
}
Employee.prototype.name = "";

function WorkerBee () {
  this.projects = [];
}
WorkerBee.prototype = new Employee;

var amy = new WorkerBee;

Employee.prototype.name = "Unknown";
amy.name = 'unknown'
```

在访问一个对象的属性时，JavaScript 将执行下面的步骤：

1. 检查对象自身是否存在。如果存在，返回值。

2. 如果本地值不存在，检查原型链（通过 `__proto__` 属性）。//递归检查

   //`__proto__`指向继承对象的prototype

3. 如果原型链中的某个对象具有指定属性，则返回值。

4. 如果这样的属性不存在，则对象没有该属性，返回 undefined。

###### 34.generator函数：能够return多次的函数

​	定义：

```js
function* foo(x){
    yield x+1;
    yield x+2;
    return x+3;//return要在最后，否则return后面的yield不能返回
}
```

​	调用：yield阻塞函数执行，next恢复执行

```js
let a = foo(1);
a.next();//{value: 2, done: false}
a.next();//{value: 3, done: false}
a.next();//{value: 4, done: true}
a.next();//{value: undefined, done: true}
```

​	或：

```js
for (let x of foo(1)){
    console.log(x)//2,3。不会打印出return的内容
}
```

在一个generator函数中执行另一个generator函数

```js
function* foo(){
	yield 'aa';
}

function* bar(){
	yield* foo();
    yield 'bb';
}
for(let val of bar()){
    console.log(val);//aa,bb
}
```

​	yield用在另一个表达式中要加（）

​	`let str = 'hello'+(yield 123)`



generator函数自动执行模块：co

```js
var co = require('co')
co(foo);//返回Promise对象

co(foo).then(()=>{
	//some code
})
```

###### 35.箭头函数嵌套(类似闭包)

```js
let add = (a)=>(b)=>a+b
let add = function(){
    
}
add(1)(2)//3

```

###### 36.form的onSubmit会默认刷新页面，使用e.preventDefault()可以阻止自动刷新

###### 37.手动用Promise封装XMLHttpRequest

```js
const url = 'http://localhost:3000'

function ajax(method,suffix,data){
    return new Promise(function(resolve,reject){
        const handler = function(){
            if(xhr.readyState !== 4){
                return
            }
            if(xhr.status === 200){
                resolve(xhr.responseText)
            }else{
                reject()
            }
        }
        let xhr = new XMLHttpRequest()
        xhr.open(method,url+suffix)
        xhr.setRequestHeader('Content-Type','application/json;charset=utf-8')
		xhr.send(data)
        xhr.onreadystatechange = handler
    })
}

ajax('GET','/user','').then().catch()
```

###### 38.字符串加数字：把数字转成字符串拼接；字符串减数字：把字符串转成数字运算

```js
'11'+1 //'111'
'11'-1 //10
```

###### 39.js的addEventListener与removeEventListener

```js
window.addEventListener('scroll',this.handleScroll)
//等同于onScroll
window.removeEventListener('scroll',this.handleScroll)
//移除事件监听的时候要指定后面的函数，否则不行。因此add的时候不能使用匿名函数
```

###### 40.es6动态改变元素类名

```jsx
<div className={`test ${tiaojian?'active':''}`}></div>
```

###### 41.js判断数组维度

一维二维

```js
const tf = arr => arr.some(item=> item instanceof Array)
tf(arr)//true则为二维数组

Array.some()//只要数组中有一个满足条件就返回true，不继续对剩下的元素执行	
```

判断任意维

```js
function dimension(arr){
	if(arr instanceof Array){
        return Math.max(...arr.map(e=>{
            return 1+dimension(e)
        }))
    }else{
        return 0
    }
}
```

###### 42.setTimeout(function,1000)，function一定不能立即执行，即不能加（）
###### 42.类装饰器

```typescript
// 装饰器的原理
@decorator
class A {}

//等同于

class A {}
A = decorator(A) || A;
```

###### 43.n维数组降维

`let arr = [1,2,7,3,[3,4,[5,4,6]]]`

```js
Array.from(new Set(arr.flat(Infinity)))//降维去重
```

或

```js
function flatten(arr1){
	return arr1.reduce((r,item)=>Array.isArray(item)?r.concat(flatten(item)):r.concat(item),[])
}

Array.from(new Set(flatten(arr)))
```

###### 44.数组排序

```js
Array.from(new Set(flatten(arr))).sort((a,b)=>{return a-b})
//[1,2,3,4,5,6,7]
```

###### 45.[object] instanceof [构造函数]

​	若左侧为基本类型，则直接返回false，例如：`1 instanceof Number`，结果为false

###### 46.typeof 返回一个字符串，表明类型（只能判断基本数据类型）

​	注意：

```js
typeof [1,2,3] //"object"
typeof null //"object"
```

###### 47.各种循环break

```js
let a = [1,2,3,4,5,6]
//不会break
a.forEach(item=>{
  if(item ===3){
    return
  }
  console.log(item)
})

//可以break
for(let i = 0;i<a.length;i++){
  if(a[i] === 3){
    break
  }
  console.log(a[i])
}
//可以break
a.every(item=>{
  if(item ===3){
    return false
  }else{
    console.log(item) 
    return true
  }
})
//可以break
a.some(item=>{
  if(item ===3){
    return true
  }
  console.log(item)//1，2，true
})

```

###### 48.js删除对象的某一属性

```js
let obj = {
	attr1:11
}
delete obj.attr1
//最好按以下方式设置
obj.attr1 = ''  
```

###### 49.es6的单例写法

```js
class Db {
    //ES6类的静态方法（只能直接由类名调用的方法）：static getInstance
    //ES6类的静态属性：直接挂载在类名上的方法，如：Db.instance()
    static getInstance() {
        if (!Db.instance) {
            Db.instance = new Db();
            return Db.instance
        }
        return Db.instance;
    }
    constructor(name, age) {
        this.name = name;
        this.age = age;
        //在constructor里面可以初始化地（对象一创建就开始）运行对象的方法
        this.connect()
    }
    connect() {
        console.log("I am sillyB,我连接上了数据库")
    }
    find() {
        console.log("查询数据库")
    }
}
//单例模式创建对象时，不再使用类直接创建对象，而是使用类名调用类的静态方法来创建（或返回）对象
var db1 = Db.getInstance()
var db2 = Db.getInstance()
var db3 = Db.getInstance()
db1.find()
db2.find()
db3.find()
/*结果：
I am sillyB,我连接上了数据库
查询数据库
查询数据库
查询数据库*/
```

###### 50.js取整

Math.round()在小数部分恰好等于0.5的时候舍入到相邻的正无穷方向上的整数，会导致例如

Math.round(-1.5)  //-1

所以需要在这种情况做一下处理

```js
function round(num){
      if(num.toString().indexOf('.')<0){
        return num
      }else{//负数，且小数部分刚好是0.5
        let abs_num = Math.abs(num)
        let a = abs_num-Math.floor(abs_num)
        if(num<0&&a===0.5){
          return Math.round(num)-1
        }else{
          return Math.round(num)
        }
      }
    }
```

###### 60.toString()检测对象类型：Object.prototype.toString.call(thisArg)

```js
var toString = Object.prototype.toString;

toString.call(new Date); // [object Date]  字符串
toString.call(new String); // [object String]
toString.call(Math); // [object Math]

//Since JavaScript 1.8.5
toString.call(undefined); // [object Undefined]
toString.call(null); // [object Null]
```

###### 61.[Object.assign()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

###### 62.es6链判断运算符  ?.

​	**存在定义则继续调用，否则返回undefined**

​	三种用法

```
obj?.prop
obj?.[expression]
func?.()
```

​	如果读取对象内部的某个属性，往往需要判断一下该对象是否存在，例：

```
const  firstName = message.body.user.firstName  //错误写法，如果内部不存在对应属性，则会报错
const firstName = (message
  && message.body
  && message.body.user
  && message.body.user.firstName) || 'default'; // 正确的写法
const  firstName = message?.body?.user?.firstName ?? 'default' //es6正确写法
```

​	判断方法是否存在，存在就执行

```
const a = 0
a?.()   // Uncaught TypeError: a is not a function

const a = ()=>{console.log(1)}
a?.()  // 1
```

###### 63.es6null判断运算符  ??

读取对象属性的时候，如果某个属性的值是`null`或`undefined`，有时候需要为它们指定默认值。常见做法是通过`||`运算符指定默认值。

```javascript
const a = ''
const c = a || 'Hello, world!'; //c='Hello, world!'
```

上面代码通过`||`运算符指定默认值，但是这样写是错的。开发者的原意是，只要属性的值为`null`或`undefined`，默认值就会生效，但是这里属性的值如果为空字符串或`false`或`0`，默认值也会生效。

为了避免这种情况，[ES2020](https://github.com/tc39/proposal-nullish-coalescing) 引入了一个新的 Null 判断运算符`??`。它的行为类似`||`，但是只有运算符左侧的值为`null`或`undefined`时，才会返回右侧的值。

```javascript
const a = ''
const c = a ?? 'Hello, world!';  //c=''
```

上面代码中，默认值只有在左侧属性值为`null`或`undefined`时，才会生效。

###### 64.js数据类型

基本数据类型Number、String、Boolean、Symbol、Undefined、Null

引用数据类型Object，包括Funtion、Array

###### 65.判断点击事件是否在一个元素内

```js
document.addEventListener('click', (e) => {
	const target = document.getElementById('target')
	if(target == e.target||target.contain(e.target)){
		//在目标元素内部
	}else{
		//不在
	}
}
```

###### 66.函数简写

```js
const ff = x=>x*2
//相当于
const ff = x=>{return x*2}
```

###### 67.防抖、节流简单实现

```js
const debounce = function(func,ms){
    let timer = ''
    return ()=>{
		if(timer){
            clearTimeout(timer)
        }
        timer = setTimeout(func,ms)
    }
}

const throttle = function(func,ms){
    let flag = true
    return ()=>{
        if(!flag) return
        flag = false
        setTimeout(()=>{
            func()
            flag = true
        },1000)
    }
}
```

###### 68.this指向问题

普通函数中的this指向调用者，即调用时才确定

箭头函数中的this在定义时就确定了，即定义时所在作用域指向的对象

**注：对象不构成作用域**

###### 69.new

1.创建空对象

2.将空对象的__proto__指向构造函数的原型对象

3.将构造函数的this指向创建的对象

4.返回该对象

```js
function Test(a) {
	this.a = a
}

const t = new Test('aa')
//等价于
let obj = {}
obj.__proto__ = Test.prototype
const t = Test.call(obj,'aa')
```



# TypeScript

###### 1.ts中一个数组中的元素类型必须一致

​	元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 

```typescript
let x:[string,number]
x=['hello',1]

//联合类型，数组越界访问时使用联合类型
x[3] = 'world' //ok
x[3] = true //error
```

###### 	若一个数组声明为any，则可以是不同类型的元素

```typescript
let list: any[] = [1, true, "free"];//此时就相当于是js
list[1] = 100;
```

###### 2.枚举类型（enum）

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green; //c = 1
let colorName:string = color[1];//colorName = Green
```

###### 3.类型断言(类似于类型转换)

```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```



# react-router

###### 1.onEnter()、onLeave()路由进入，离开时进行一些处理。v4已经移除

###### 2.router的history只在route中挂载的组件中有定义，如果是公共组件，例如Header中要进行路由，需要在引用Header的组件中传递history属性,或者使用withrouter

```jsx
<Header currentpage="home" history={this.props.history}/>
```

###### 3.页面传值

​	1.url参数

​	2.query/state

​		route定义

```jsx
<Route path='/query' component={Query}/>
```

​		Link组件

```jsx
var query = {
        pathname: '/query',
        query: '我是通过query传值 '//可以是对象
}

<Link to={query}>query</Link>
```

​		参数获取：`this.props.location.query`

###### 4.路由跳转的时候给出提示信息

```jsx
import {Prompt} from 'react-router-dom'
<Prompt 
  when={bool}
  message={string/function}
/>
```



# [webpack](https://webpack.docschina.org/concepts/)

###### 1.config引入css-loader顺序

​	主要问题是配置loader的时候要按顺序写。style-loader、css-loader、less-loader

###### 2.create-react-app搭建的脚手架，需要run eject才能暴露出配置文件

###### 3.webpack entry

​	单页面应用一个入口，多页面应用可以配置多个入口



​	entry传入一个数组？

```
entry:{
	main:['./app.js','lodash']
}
```

​	**数组中的文件一般是没有相互依赖关系的，但是又处于某些原因需要将它们打包在一起。(即多个文件打包成一个chunk)**

###### 4.如果要根据 webpack.config.js 中的 **mode** 变量更改打包行为，则必须将配置导出为一个函数，而不是导出为一个对象：

```js
var config = {
  entry: './app.js'
  //...
};

module.exports = (env, argv) => {
  if (argv.mode === 'development') {
    config.devtool = 'source-map';
  }
  if (argv.mode === 'production') {
    //...
  }
  return config;
};
```

​	自我理解：相当于配置多个config文件，如：webpack.config.pro.js，webpack.config.dev.js

###### 5.缓存优化相关配置

​	浏览器通过命中缓存，降低网络流量。=>bundle分离。

​	按如下方法

​	1.输出文件文件名使用可替换模板字符串：

```
output:{
	filename:'[name].[contenthash].js',
}
```

​	2.bundle分离

```js
    optimization: {
     runtimeChunk: 'single',//将webpack运行时引导代码提取出来一个单独的bundle
     splitChunks: {//分离静态依赖模块
       cacheGroups: {
         vendor: {
           test: /[\\/]node_modules[\\/]/,
           name: 'vendors',
           chunks: 'all'
         }
       }
     }
    }
```

​	此时修改本地依赖（自己的代码）,vendors输出文件的hash值还是会变，期望是不变的（这样缓存才能命中）。可以加入以下内容

```js
const webpack = require('webpack')

plugins:[
	new webpack.HashedModuleIdsPlugin()
]
```

###### 6.webpack详细配置参数

​	[webpack](https://webpack.docschina.org/configuration/output/)

###### 7.模块热替换HMR（局部刷新，无需全部刷新）

​	只配置devserver可以实现自动刷新，但是是完全刷新的。

​	[react插件react-hot-loader](https://github.com/gaearon/react-hot-loader)，使用babel的方式（react懒加载）

###### 8.publicPath

###### 9.hash、chunkhash、contenthash区别

<img src="D:\projects\jsnote\image-20210105104738748.png" alt="image-20210105104738748" style="zoom:80%;" />

![image-20210105104733343](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210105104733343.png)

###### 10.打包分析

```
npm run build -- --report
```

###### 11.require.context()

如果想引入一个文件夹下面的所有文件，或者引入能匹配一个正则表达式的所有文件，这个功能就会很有帮助

```js
const context =  require.context('./components',false,/\.vue$/) //三个参数：文件夹，是否搜索子目录，匹配文件的正则

let m = {}
context.keys().forEach((key)=>{
    m[key] = context(key)
})
```

###### 12.vue官方提供的自动化全局注册方式(require.context())

```js
import Vue from 'vue'
import upperFirst from 'lodash/upperFirst'
import camelCase from 'lodash/camelCase'

const requireComponent = require.context(
  // 其组件目录的相对路径
  './components',
  // 是否查询其子目录
  false,
  // 匹配基础组件文件名的正则表达式
  /Base[A-Z]\w+\.(vue|js)$/
)

requireComponent.keys().forEach(fileName => {
  // 获取组件配置
  const componentConfig = requireComponent(fileName)

  // 获取组件的 PascalCase 命名
  const componentName = upperFirst(
    camelCase(
      // 获取和目录深度无关的文件名
      fileName
        .split('/')
        .pop()
        .replace(/\.\w+$/, '')
    )
  )

  // 全局注册组件
  Vue.component(
    componentName,
    // 如果这个组件选项是通过 `export default` 导出的，
    // 那么就会优先使用 `.default`，
    // 否则回退到使用模块的根。
    componentConfig.default || componentConfig
  )
})
```



# Git学习

1.git clone 克隆远程仓库,克隆特定分支加上-b branch_name

2.创建自己的分支并切换到此分支： git checkout -b your_branch

​	创建并切换分支，同时指定远程仓库的源分支(创建的分支从远程clone，不是从当前分支) ：

​	git checkout -b your_branch origin/branchname

```bash
创建一个全新的分支（不包含历史提交记录），git checkout --orphan test
删除所有文件  git rm -rf .
```

3.上传自己的分支到远程仓库：git push origin your_branch（本地）:your_branch（远程）

​    本地分支与远程分支建立关联：`git push --set-upstream origin your_branch`，建立	关联之后后面就可以直接push了（不用后缀）

4.直接拉取远程分支：`git pull origin branch_name`

5.git fetch和git pull的区别：fetch获取不合并，pull获取且合并

6.删除本地分支：先切换到别的分支，然后`git branch -d your_branch`

​	强制删除本地分支： `git branch -D your_branch`

7.删除远程分支： `git push origin --delete branch_name`

8.git ssh避免每次pull、push都输密码：在生成公钥的时候不输密码

9.git创建ssh  `ssh-keygen -t rsa -C “邮箱”`，然后复制.ssh/id_rsa.pub里的内容，添加到github账户里

10.git pull拉远程分支，冲突但不想手动一git 个个解决冲突（此时也无法切换到别的分支），使用git merge --abort可以回复到pull之前的状态

11.`git rebase dev`:把dev分支的改动合并到当前分支

12.`git commit --amend -m 'message'`修改上次提交的信息

13.`git add . `暂存更改到暂存区。`git checkout .` 恢复暂存区文件到工作区。

14.版本回退到上一个commit，`git reset --hard HEAD^`

15.`git push --set-upstream  origin branchname`设置本地当前分支的默认上传分支

16.`git commit -am 'message'`把所有更改提交，省略了`git add .`

17.本地删除远程仓库

```powershell
git rm -r --cached node_modules//删除node_modules文件夹
git commit 
git push
```

18.本地代码上传：1.远程创建仓库tests；2.本地如下操作

**注意：远程创建仓库的时候不要添加readme**

![](./1575273396358.png)

​	-u后续推送只需要git push

19.从远程特定的分支clone

```
git clone -b branchname ssh://....
```

20.git stash暂存    git stash pop（弹出：出栈）/apply(取出，不出栈)

```
git stash show //显示stash的内容（每个文件的差异+++++-----）
git stash show -p //显示具体的更改（每一行）
git stash show -p stash@{1} //显示特定的某个stash，注意在vscode中执行可能出错，要在git bash中执行
```



21.git导出commit日志,[参数参考](https://git-scm.com/docs/pretty-formats)

```
 git log --pretty=format:"%h %an %as %s %b"  --encoding=gbk >log.csv

%h   简略hash

```

中文乱码时设置

```
 git config --global i18n.logOutputEncoding gbk
```

但这个设置会使git log输出乱码，可以用下面恢复

```
 git config --global i18n.logOutputEncoding utf-8
```



22.撤销commit

```
git reset --soft HEAD^ //撤销commit，不撤销git add .
git reset --mixed HEAD^ //撤销commit，撤销git add .
```

23.git log --pretty=format:"%h %s" --graph（以树状图形式展示分支、合并历史）

24.打tag

```
git tag -a v1.0 //可以添加附注
git tag v1.0 //轻量级，无需添加附注
git tag -d v1.0//删除tag
```

25.git describe --long --dirty --tag

如果不加--tag则只显示带注释的标签

26.[git clone fatal: Authentication failed for "xxx"](https://blog.csdn.net/yphust/article/details/100542265)

27.git reflog

Reference logs, or "reflogs", record when the tips of branches and other references were updated in the **local repository**

记录本地所有变更历史
28.git push失败，提示输密码http://www.79tui.com/happy/741509.html

29.gitignore

忽略某个动态生成名字的文件夹

/dist*

# Gerrit

abandon会丢掉当前patch set所在的change，慎用！

git pull是从git仓库拉的  不是gerrit

gerrit不允许跳过change合并

git checkout 特定的文件



git push origin HEAD:refs/for/develop

设置直接git push，在`.git/config`中编辑，新增

```
[remote "origin"]
	push = refs/heads/*:refs/for/*
```



# CSS问题

###### 1.去除（微信）页面左右滑动：

```css
width:100%;
overflow-x:hidden;
```

###### 2.多行文本设置垂直居中：

**absolute是相对于该元素的第一个定位为非static的父元素**

不定宽高的盒子（son）水平垂直居中

```html
.parent{
	position:relative;
	height:100px;
	width:100px;
}
.son{
	positon:absolute;
	top:50%;
	left:50%;
	transform:translate(-50%,-50%);
}

<div class="parent">
    <div class="son">
        文本
    </div>
</div>
```

flex布局水平垂直居中

```css
display:flex;
justify-content: center; /* 水平居中 */
align-items: center;     /* 垂直居中 */
```



###### 3.react内联图片背景设置

```css
style={{background:`url(${self.state.adpic})`}}
```



###### 5.实现两翼固定，中间自适应

```html
<!-- DOM结构 -->
<div id="container">
  <div id="center"></div>
  <div id="left"></div>
  <div id="right"></div>
</div>
```

```css
#container{
    display:flex
}
#left{
	width:100px
}
#right{
    width:100px
}
#center{
	flex:1	
}
```

​	或

```css
#container{
	display:table
}
#container>div{
	display:table-cell
}
#left{
    width:100px
}
#center{
    
}
#right{
    width:100px
}
```



###### 6.两个DOM元素的显示顺序：z-index

1. **如果是在相同的层叠上下文，按照层叠水平的规则来显示元素**
2. **如果是在不同的层叠上下文中，先找到共同的祖先层叠上下文，然后比较共同层叠上下文下这个两个元素所在的局部层叠上下文的层叠水平。**  

###### 7.设置子元素定位相对于父元素：要设置父元素的position！（relative)

###### 8.a标签跳转会重新加载全部资源，影响性能，使用路由会快很多

###### 9.footer问题

​	当页面内容不够时放在页面最底部，当页面内容很多时，往下滑动才能看到：

​	设置样板页面（index.html）的body，root的`height:100%`，同时当前页面（home）的html，	body`height:100%`，然后设置home最顶层容器

```css
    box-sizing: border-box;
    min-height: 100%;
    position: relative;
    padding-bottom: 26px;(footer的高度)
```

​	最后设置footer

```css
	posotion:absolute;
	height:26px;
	bottom:0;
```

###### 10.rotate

​	应该使用`transform:rotate(7deg)`,不要直接使用rotate(7deg)!!!!

###### 11.ios全面屏底部适配

```js
function isIPhoneX(fn) {
    var u = navigator.userAgent;
    var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
    if (isIOS) {
        if (screen.height >= 812 && screen.width >= 375) {//像素判断
            $('.xshop-main-container').css('bottom', '70px');
            $('.xshop-main-navs').css("height", "70px");
        }
    }
}
```

###### 12.相邻border合并

​	方法1.设置display:table，border-collapse:collapse

​	方法2.把要合并方向的其中一个margin设置为负的border宽度，如

```css
    border: 1px solid #eaeaea;
    margin-bottom: -1px
```

###### 13.页面底部有fixed的元素会遮挡主体部分：设置主体部分padding-bottom

###### 14.前端怎么保留接收到的文本中的换行符↵

```html
<pre>{content}</pre>
```

```css
pre{
   	white-space:pre-wrap
    word-wrap: break-word;
}
```

###### 15.ios软键盘无法弹起底部输入框

###### 16.内部元素浮动，外层容器无法被撑开

​	方法1：父元素设置`overflow:hidden/auto`

​	原理：触发父元素的BFC属性

​	bfc特性：

​	**a.阻止外边距折叠**

​	**b.可以包含浮动的元素**

​	**c.可以阻止元素被浮动元素覆盖**

​	方法2：父元素设置`::after{clear:both;content:'';display:block}`

###### 17.position:absolute/fixed

​	流式布局里，absolute的元素随着页面下拉会隐藏，但是fixed的元素会一直在窗口中

###### 17.positon:sticky（初始relative，达到条件变成fixed定位）

页面滚动图片覆盖

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <style>
      div{
          position:sticky;
          top:0;//条件
      }  
  </style>
</head>
<body>
<div><img src="https://picsum.photos/id/10/480/360"></div>
<div><img src="https://picsum.photos/id/11/480/360"></div>
<div><img src="https://picsum.photos/id/12/480/360"></div>
<div><img src="https://picsum.photos/id/13/480/360"></div>
<div><img src="https://picsum.photos/id/14/480/360"></div>
</body>
</html>
```



###### 18.box-sizing:border-box

​	**width(宽) + padding(内边距) + border(边框) = 元素实际宽度**

​	**height(高) + padding(内边距) + border(边框) = 元素实际高度**

设置该属性后padding和border就包含在实际设置的宽高中，即设置padding和border不会扩大元素宽高

###### 19.为一个元素设置两个class，要使css生效需要把两个类名连在一起写

```css
.class1.class2{//正确
    
}

.class1 .class2{//错误，这是父子选择
    
}
```

###### 20.css ~ , +  >

​	A~B:为所有和A具有相同父元素的B设置样式

​	A+B:为紧邻着A的B设置样式，AB须有相同的父元素

​	A B：选择A所有的后代B元素 

​	A>B：选择A的一代B元素 

​	AB：为同时有ab两个类名的元素设置样式

	A,B：为AB同时设置样式
###### 20.回流，重绘

当`Render Tree`中部分或全部元素的尺寸、结构、或某些属性发生改变时，浏览器重新渲染部分或全部文档的过程称为**回流**。

当页面中元素样式的改变并不影响它在文档流中的位置时（例如：`color`、`background-color`、`visibility`等），浏览器会将新样式赋予给元素并重新绘制它，这个过程称为**重绘**。

**如何避免**

**css**

- 避免使用`table`布局。
- 尽可能在`DOM`树的最末端改变`class`。
- 避免设置多层内联样式。
- 将动画效果应用到`position`属性为`absolute`或`fixed`的元素上。
- 避免使用`CSS`表达式（例如：`calc()`）。

**javascript**

- 避免频繁操作样式，最好一次性重写`style`属性，或者将样式列表定义为`class`并一次性更改`class`属性。
- 避免频繁操作`DOM`，创建一个`documentFragment`，在它上面应用所有`DOM操作`，最后再把它添加到文档中。
- 也可以先为元素设置`display: none`，操作结束后再把它显示出来。因为在`display`属性为`none`的元素上进行的`DOM`操作不会引发回流和重绘。
- 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
- 对具有复杂动画的元素使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁回流。

###### 21.top/margin-top

​	top一般结合position:absolute使用（只在static时无效）

​	margin-top一般结合position:relative使用

###### 22.禁用浏览器缩放（只缩放目标元素）

```css
#app{
    touch-action:none
}
```

###### 23.margin:auto

​	若只设置左右一边`margin-right:auto`则对应外边距占满所有可用空间

###### 24.伪元素、伪类

伪类单冒号

伪元素建议都使用双冒号

# vscode

###### 1.替换所有文件中的某一匹配项

​	编辑->在文件中替换

###### 2.settings.json

​	添加插件后可以在这个文件自定义插件的配置

###### 3.中文匹配

```
(.[\u4E00-\u9FA5]+)|([\u4E00-\u9FA5]+.)
```



# node.js

###### 1.path

```js
path.join()//直接拼接
path.resolve()//生成绝对路径
path.relative(from,to)//返回从from到to的相对路径  例如：/data/heloo,/data/nihao。返回../nihao
```

[]: https://blog.csdn.net/kikyou_csdn/article/details/83150538	"path"

###### 2.nvm控制node版本

​	1.从官方github下载nvm安装包，默认安装

​	2.设置淘宝镜像https://blog.csdn.net/kezanxie3494/article/details/80248649

​	3.`nvm install version`

​	4.`nvm use version`

​	查看当前安装的node版本`nvm list`

​	**5.windows下nvm安装8.11以上版本的node，都不能自动安装好对应的npm！！**

​	这会导致不能使用npm

​	需要自己去下载对应的npm版本    [解决办法](https://blog.csdn.net/Deleven_Blog/article/details/100077732)

###### 3.eslint:代码检查、规范工具

###### 4.node.js用法

​	作为服务器端在大型项目中一般是作为中间层转发(web服务器)以及一些处理

​	前端页面-->node（web）服务器-->后端（python、java等）

​	![web架构](./web架构.png)

​	node也可以作为后端使用，直接作为业务逻辑层处理数据返回给前端请求。**node.js适合运用在高并发、I/O密集、少量业务逻辑的场景**

# react

###### 1.父组件调用子组件内部方法：（ref）

```jsx
// Child
class Child extends Component {
    childFunction() {}
}

class Parent extends Component {
    // 调用
    parentFunction() {
        this.child.childFunction();
    }

    render() {
        return (
            <Child ref={(child) => { this.child = child; }} />
        );
    }
}
```

###### 2.使用变量控制元素是否显示

```js
this.state.show&&<div/>//要确保this.state.show为布尔值，不能是0，0会被正常识别并渲染
```

###### 3.react.pureComponent和react.memo()

- React.PureComponent是给ES6的类组件使用的
- React.memo(...)是给函数组件使用的
- React.PureComponent减少ES6的类组件的无用渲染     //浅比较，引用类型只比较地址
- React.memo(...)减少函数组件的无用渲染
- 为函数组件提供优化是一个巨大的进步

###### 4.react受控组件

​	**渲染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”。**

​	select元素设置默认选中项

```jsx
      <form onSubmit={this.handleSubmit}>
        <label>
          选择你喜欢的风味:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">葡萄柚</option>
            <option value="lime">酸橙</option>
            <option value="coconut">椰子</option>
            <option value="mango">芒果</option>
          </select>
        </label>
        <input type="submit" value="提交" />
      </form>
 
```

​	成熟的表单解决方案：Formik

###### 5.Fragment标签

```jsx
<React.Fragment></React.Fragment>
//可以用空标签代替使用，如下。但是空标签不能添加key和属性
<></>
```

###### 6.immutable.js

​	![1572247668283](./1572247668283.png)

###### 7.setState({[key]:'xxx'}),key为变量时的设置方法

###### 8.Hook(函数组件中使用state等特性)

​	hooks必须写在函数最外层，不能写在ifelse等语句中。因为useState是根据顺序来赋值的，如果有条件判断会出错

```jsx
let tof = true

const [count,setCount] = useState(6)//初始值6
if(tof){
    const [test,setTest] = useState(55)
    tof = !tof
}
const [test1,setTest1] = useState(66)
//报错
```



```jsx
useEffect(()=>{//相当于componentDidMount，componentDidUpdate 和 componentWillUnmount 这三个函数的组合。在每次渲染后都会执行
    //dosomething
    
    return ()=>{//useEffect返回的函数为清除副作用的函数，组件卸载和更新时调用
        //dosomething。取消订阅，清楚定时器等
    }
},[param])//第二个参数表示只在param改变的时候才会调用当前effect。若数组为空，则effect只会在挂载和卸载的时候执行
```

自定义Hook：use开头，另写一个function组件

###### 9.公共逻辑提取出来，例如支付

pay.js

```jsx
let Pay = {}
Pay.func1 = ()=>{
    
}

export default Pay
```

###### 10.HOC/render props(复用)

HOC:**高阶组件是参数为组件，返回值为新组件的函数。**

<!--redux的connect函数就是HOC-->

提取公共逻辑->放在HOC中->HOC包裹，并将方法作为属性传给子组件

不能在HOC中修改子组件

###### 11.react-router&react-router-dom

# vue

###### 1.vue是响应式的，但不能响应数组和对象内部变化（直接赋值），若要实现响应可按下面操作

```js
//对象
Vue.set(vm.someObject, 'b', 2)  
this.$set(this.someObject,'b',2) //this.$set是全局vue.set的别名
this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })//需将两者合并到一个新的空对象中才行，否则Object.assign(this.someObject, { a: 1, b: 2 })也不会触发更新

//数组
//Vue 不能检测以下数组的变动：
//当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue
//当你修改数组的长度时，例如：vm.items.length = newLength
//用vue的set方法或数组的splice方法改变数组
Vue.set(this.items, indexOfItem, newValue)
this.items.splice(indexOfItem, 1, newValue)
```

###### 2.nextTick（）

​	在下次 DOM 更新循环结束之后执行**延迟回调**。

###### 3.按需引入lodash

1. 安装

   ```
   npm install lodash --save
   npm install lodash-webpack-plugin babel-plugin-lodash --save-dev
   ```

   2.修改babel配置

```
"plugins": ["lodash"]
```

3.修改webpack配置

```
const LodashModuleReplacementPlugin = require('lodash-webpack-plugin')
  plugins: [
    new LodashModuleReplacementPlugin()
  ]
```

###### 4.事件传参

```vue
@change($event,others)  //$event是默认参数
```

###### 5.$attrs

​	子组件接收到的非props属性

# vue3.0

###### 1.v-model?

# 其他

###### 1.浏览器缓存机制

![](./浏览器缓存机制.png)

###### 2.禁止chrome自动填充

自动填充机制：**页面里有一个type=password的input且这个input前面有一个type=text的input的时候就会进行自动填充**

```jsx
<input autoComplete='new-password'></input>
```

上述办法可以阻止浏览器自动填充，但是当focus到password栏的时候，选择保存的密码会把相邻的上一栏内容覆盖，解决办法：

在type = password的输入框上面加两个隐藏的输入栏，不能使用display：none

```html
<input style="opacity: 0;position:absolute;width:0;height:0;">//默认type='text'
<input type="password" style="opacity: 0;position:absolute;width:0;height:0;">
```

###### 3.service worker（PWA）

​	workbox

###### 4.IndexedDB

​	浏览器数据库。可以将大量的数据存储在客户端

###### 5.动画问题

​	简单的动画用css

​	复杂的用js

###### 6.跨域

​	**跨域并不是请求发不出去，请求能发出去，服务端能收到请求并正常返回结果，只是结果被浏览器拦截了**

**解决方式：**

​	1.jsonp只支持get请求

​	2.**跨域资源共享（CORS）**（静态资源？）:nginx设置response-header

​	3.nginx反向代理（http请求，nginx做转发）

​		正向代理：代理客户端

​		反向代理：代理服务器



​	**设置document.domain解决无法读取非同源网页的 Cookie问题**

```js
// 两个页面都设置  仅限主域相同，子域不同的跨域应用场景
document.domain = 'test.com';
```

###### 7.锚点:页面跳到指定位置

​	url中加元素id

```
localhost#id
```

###### 8.页面间跳转记录当前页面位置

​	sessionStorage

###### 9.本地上传图片，未经后台处理，实时预览

```jsx
<input type='file' onChange={(e)=>{
     let URL = window.URL || window.webkitURL
     let imgurl = URL.createObjectURL(e.target.files[0])
     this.setState({imgurl})
}}/>
<img src={this.state.imgurl}/>
```

###### 10.响应式布局

​	1.rem

###### 11.ssr一般只做首屏渲染（SEO优化）


###### 12.nginx

​	重启服务nginx -s reload

​	
###### 12.antd form的自定义validator注意事项

规则：

1. 最后必须callback一个信息回来
2. 如果效验时代码出错会导致全部规则失效

```js
validator:(rule: any, value:string, callback: Function) => {
// if(!value){
//     callback()
// }
//保证自定义validator一定不会出错从而导致表单提交的时候validateFieldsAndScroll无法执行
//采用下面的try catch，或者像上面一样value为空时callback()
//下面方法还有一个优点是在调试的时候可以定位错误，否则antd本身不会报哪个自定义validator出错

    try{
        if(value.length>50){
            callback('最多输入50字')
        }else
            callback()
    }catch(err){
        callback()
    }
}
```

**总结：就是每一种情况都要考虑到，否则就会出问题，为了避免自己逻辑不周全就直接采用try catch了**

###### 13.path-to-regexp使用

```jsx
var pathToRegexp = require('path-to-regexp')

var reg = pathToRegexp(url) //把url转换成正则表达式，返回转换后的正则表达式
reg.exec(url)//匹配
pathToRegexp.parse(url)//解析url参数

var url = '/user/:id/:name'
var data = {id: 10001, name: 'bob'}
pathToRegexp.compile(url)(data)//输出/user/10001/bob
```

###### 14.[svg path](https://segmentfault.com/a/1190000009556665)

```vue
<svg width="100%" height="100%">
 <path d="M0,0 L240,0 L240,240 L0,240 Z" fill="#fff" stroke="#000" stroke-width="10" transform="translate(5,5)"></path>
</svg>
M = moveto(M X,Y) ：将画笔移动到指定的坐标位置
L = lineto(L X,Y) ：画直线到指定的坐标位置
H = horizontal lineto(H X)：画水平线到指定的X坐标位置
V = vertical lineto(V Y)：画垂直线到指定的Y坐标位置
C = curveto(C X1,Y1,X2,Y2,ENDX,ENDY)：三次贝赛曲线
S = smooth curveto(S X2,Y2,ENDX,ENDY)：平滑曲率
Q = quadratic Belzier curve(Q X,Y,ENDX,ENDY)：二次贝赛曲线
T = smooth quadratic Belzier curveto(T ENDX,ENDY)：映射
A = elliptical Arc(A RX,RY,XROTATION,FLAG1,FLAG2,X,Y)：弧线
Z = closepath()：关闭路径
```

###### 15.复制chrome控制台变量

```
javascript:(function(){
	document.addEventListener('copy', function fn(e){
		document.removeEventListener(e.type,fn);
		let data = JSON.stringify(temp1);
		console.log('开始拷贝')
		e.clipboardData.setData('text/plain',data);
		e.clipboardData.setData('text/html', data);
		e.preventDefault();
		console.log('拷贝成功')
		console.log(data)
	});
	// 自动触发复制事件,低版本浏览器不支持的事件
	 document.execCommand('copy');
})()
```

###### 16.fetch()/axios

fetch是es6中新提出的api，是xhr的替代方案

axios是基于xhr封装的库

###### 17.http短连接、长连接

tcp：传输层

http：应用层

七层：物理层、数据链路层、网络层、传输层、会话层、表示层、应用层

**实质上是tcp的短连接和长连接**

短连接：每次建立http连接都需要重新建立tcp连接

长连接：可以复用已建立的tcp连接，开启长连接，指定header的connection：keep-alive（http/1.1默认为keep-alive）

###### 18.Date.now()  vs new Date().getTime()

都返回时间戳，但前者比后者快

```
let t1 = new Date()
setTimeout(()=>{
	t2 = t1.getTime()
},200)

//若按上述写，t2获得的时间戳为t1声明时的时间
```

###### 19.package.json

```
"vue":"2.5.2",  指定2.5.2版本
"vue":"~2.5.2",  2.5.2以上但小于2.6的最新版本，即不改变主要和次要版本号
"vue":"^2.5.2",  2.5.3以上但小于3.0的最新版本，即不改变主要版本号
```

###### 20.elementui的 button文字不居中，可能是因为宽度太小

###### 21.本地存储

indexDB:localForage

# 小程序开发

###### 1.小程序中使用weui

​	1.从官方github下载项目

​	2.解压，把weui-wxss-master\dist\style目录下的weui.wxss复制到项目根目录

​	3.在app.wxss中`@import 'weui.wxss';`

​	4.按照官方示例使用即可

​	**或**（封装的组件）

​	1.从开发文档下载所需组件，解压放入components文件夹下，在app.wxss`@import 'weui.wxss';`

​	2.在页面json中加入以下配置（使用绝对路径，从根目录开始，如下）

```json
{
  "usingComponents": {
    "mp-dialog": "/components/dialog/dialog"
  }
}
```

​	3.在对应页面wxml中直接使用

```
<mp-dialog title="test" show="{{true}}" bindbuttontap="tapDialogButton" buttons="{{[{text: '取消'}, {text: '确认'}]}}">
    <view>test content</view>
</mp-dialog>
```

###### 2.slot

​	插槽：自定义组件预留位置，以便扩展，通过name属性对应

# 正则表达式

###### 1.校验电话号码

```js
 var myreg = /^[1][3,4,5,7,8][0-9]{9}$/;
 myreg.test(15851899798)
```

###### 2.校验固定电话

```js
let reg = /0\d{2,3}-\d{7,8}/
```

###### 3.正则匹配

```js
let reg = /([0-9]+)/g //加括号返回匹配的所有值
let str = '123,456,666'
str.match(reg) //输出['123','456','666']
```



# pixi.js（bilibili跨年页面）



# 工具

gif制作工具screentogif

json比较工具 beyondcompare

###### 生成目录树插件

```
npm install -g tree-node-cli

treee -L 3 -I "node_modules|.idea|objects|.git" -a --dirs-first
```



# 前端撤销重做逻辑设计

![](undo&redo.png)



# qiankun

状态下发，从父应用的vuex中获取值，在对应的store中调用qiankun的setGlobalState

微应用内路由跳转失败：父应用劫持了路由变化，导致子应用无法跳转



**子应用webpack-dev-server配置代理无效？**

子应用发出的请求被主应用劫持，因此需要在主应用中也配置子应用所需的代理