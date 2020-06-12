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

ajax('GET','/user','')
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

###### 46.typeof 返回一个字符串，表明类型

​	注意：

```js
typeof [1,2,3] //"object"
typeof null //"object"
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

###### 2.router的history只在route中挂载的组件中有定义，如果是公共组件，例如Header中要进行路由，需要在引用Header的组件中传递history属性

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

# Git学习

1.git clone 克隆远程仓库,克隆特定分支加上-b branch_name

2.创建自己的分支并切换到此分支： git checkout -b your_branch

3.上传自己的分支到远程仓库：git push origin your_branch（本地）:your_branch（远程）

​    本地分支与远程分支建立关联：`git push --set-upstream origin your_branch`，建立	关联之后后面就可以直接push了（不用后缀）

4.直接拉取远程分支：`git pull origin branch_name`

5.git fetch和git pull的区别：fetch获取不合并，pull获取且合并

6.删除本地分支：先切换到别的分支，然后`git branch -d your_branch`

​	强制删除本地分支： `git branch -D your_branch`

7.删除远程分支： `git push origin --delete branch_name`

8.git ssh避免每次pull、push都输密码：在生成公钥的时候不输密码

9.git创建ssh  `ssh-keygen -t rsa -C “邮箱”`，然后复制.ssh/id_rsa.pub里的内容，添加到github账户里

10.git pull拉远程分支，冲突但不想手动一个个解决冲突（此时也无法切换到别的分支），使用git merge --abort可以回复到pull之前的状态

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

###### 4.display:flex

​	设置主轴（水平）对齐方式：justify-content

​	设置垂直对齐方式：align-content

​	如果设置了不能正常显示，可能是没有给容器设置宽高



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

###### 19.设置两个class，要使css生效需要把两个类名连在一起写

```css
.class1.class2{//正确
    
}

.class1 .class2{//错误
    
}
```

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
# vscode

###### 1.替换所有文件中的某一匹配项

​	编辑->在文件中替换

###### 2.settings.json

​	添加插件后可以在这个文件自定义插件的配置

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

​	

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

​	jsonp只支持get请求

​	**跨域资源共享（CORS）**:主要是服务端设置

​	nginx反向代理

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
//下面方法还有一个优点是在调试的时候可以定位错误，否则antd本身不会报哪个自定义
//validator出错
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



# pixi.js（bilibili跨年页面）



test