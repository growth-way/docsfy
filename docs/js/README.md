# JavaScript

## 简介S

### 什么是JavaScript

JavaScript 是一种具有面向对象能力的、解释型的程序设计语言。更具体一点，它是基于对象和事 件驱动并具有相对安全性的客户端脚本语言。它的主要目的是，验证发往服务器端的数据、增加 Web 互动、加强用户体验度等。

### JavaScript发展史

#### ECMAScript (基础语法)

ECMAScript 定义的只是这门语言的基础，与Web浏览器没有依赖关系，而在基础语法上可以构建更 完善的脚本语言。JavaScript的运行需要一定的环境，脱离了环境JavaScript代码是不能运行的， JavaScript只能够寄生在某个具体的环境中才能够工作。JavaScript运行环境一般都由宿主环境和执行期 环境共同构成，其中宿主环境是由外壳程序生成的，如Web浏览器就是一个外壳程序，它提供了 一个可 控制浏览器窗口的宿主环境。执行期环境则由嵌入到外壳程序中的JavaScript引擎（或称为JavaScript解 释器）生成，在这个环境中 JavaScript能够生成内置静态对象，初始化执行环境等。

#### DOM(文档对象模型)

Web浏览器自定义的DOM组件，以面向对象方式描述的文档模型。DOM定义了表示和修改文档所需 的对象、这些对象的行为和属性以及这些对象之间的关系。DOM对象，是我们用传统的方法(javascript) 获得的对象。DOM属于浏览器，而不是JavaScript语言规范里的规定的核心内容。

#### BOM(浏览器对象模型)

前面的DOM是为了操作浏览器中的文档，而为了控制浏览器的行为和操作(BOM)，浏览器还提供了 BOM（浏览器对象模型）。

## 语法格式

###  注释

```javascript
// 这里的内容就是注释
/* 这里的内容就是注释 */
/*
 也可以这样多行注释
 */
```

### 行内式

```javascript
<!-- 行内式 实现点击事件，点击后加载一个警告框 -->
<button onclick="alert('you clicked hered!!!')">click here</button>
```

### 嵌入式

```javascript
<!-- 页面加载后执行一个警告框 -->
<script type="text/javascript" charset="utf-8">
    // 页面加载后执行一个警告框
    alert('this is inner js code');
</script>
```

### 引入外部文件

```javascript
<!-- 引入外部js文件 -->
<script src="js/hello.js" type="text/javascript" charset="utf-8"></script>
```

!>我们可以将JavaScript代码放在html文件中任何位置，但是我们一般放在网页的head或者body部 分。由于页面的加载方式是从上往下依次加载的，而这个对我们放置的js代码运行是有影响的。

## JavaScript基础语法

### 语句

### 关键字

### 标识符

标识符就是一个名字，用来给变量和函数进行命名，有特定规则和规范 

规则：由 Unicode字母 、 _ 、 $ 、 数字 、 中文 组成

​	1.不能以数字开头 

2. 不能是关键字和保留字 
3.  严格区分大小写

规范：

1. 见名知意 
2. 驼峰命名或下划线规则

### 变量

变量即一个带名字的用来存储数据的内存空间，数据可以存储到变量中，也可以从变量中取出数 据。万能的盒子。

#### 变量的声明

JavaScript是一种弱类型语言，在声明变量时不需要指明数据类型，直接用var修饰符进行声明。 变量声明和赋值：

```javascript
// 先声明再赋值
 var a;
 a = 10;
 // 声明同时赋值
 var b = 20;
```

#### 变量的注意点

1. 若只声明而没有赋值，则该变量的值为undefined。

2.  变量要有定义才能使用，若变量未声明就使用，JavaScript会报错，告诉你变量未定义

3. 可以在同一条var命令中声明多个变量。

   ```javascript
   // 声明了aa, bb没有赋值 声明了cc同时赋值10
   var aa, bb, cc = 10;
   var a = 10, b = 10, c= 10;
   console.log(aa, bb, cc);
   ```

   

4. 若使用var重新声明一个已经存在的变量，是无效的。

5. 若使用var重新声明一个已经存在的变量且赋值，则会覆盖掉前面的值

6. JavaScript是一种动态类型、弱类型语言，也就是说，变量的类型没有限制，可以赋予各种类型的

### 数据类型

虽说JS是弱类型语言，变量没有类型，但数据本身是有类型的。针对不同的类型，我们可以进行不 同的操作。JavaScript 中有6 种数据类型，其中有五种简单的数据类型：undefined、Null、布尔、数值 和字符串。一种复杂数据类型Object。

#### undefined

- undefined类型的值是undefined。 
- undefined 是一个表示"无"的原始值，表示值不存在。 
- 当声明了一个变量而没有初始化时，这个变量的值就是undefined

#### null

- null类型是只有一个值的数据类型，即特殊的值null。 
- undefined派生自null，所以等值比较返回值是true。 
- 它表示空值，即该处的值现在为空，它表示一个空对象引用。

#### boolean 布尔

布尔类型有两个值：true、false。常用来做判断和循环的条件。

#### 数值型

数值型包含两种数值：整型和浮点型。

#### 字符串

```javascript
var str1 = 'sxt';
var str2 = "good";
var str3 = 'hello' + ' everybody';
```

#### 函数

函数是具有某个功能的代码块

```javascript
function f() {
 // 具有功能的代码块
 }
```

### 类型转换

很多时候，我们在进行数据运算或输出等操作时需要将数据在不同类型之间进行转换，这里我们主 要掌握数值型和字符串。

#### 数值型(转换函数)

`JS`提供了 `parseInt()` 和 `parseFloat()` 两个全局转换函数。前者把值转换成整数，后者把值转 换成浮点数。只有对String类型调用这些方法，这两个函数才能正确运行；对其他类型返回的都是 NaN(Not a Number) 。

`parseInt()`

`parseInt()` 在转换之前，首先会分析该字符串，判断位置为0处的字符，判断它是否是个有效数 字，如果不是，则直接返回`NaN`，不再继续，如果是则继续，直到找到非字符。

```javascript
console.log(parseInt("1234blue"));  // return 1234
console.log(parseInt("0xA"));  // return 10
console.log(parseInt("22.5"));  // return 22
console.log(parseInt("blue"));  // return NaN
```

`parseFloat()`

`parseFloat()` 方法与 `parseInt()` 方法的处理方式相似，从位置 0 开始查看每个字符，直到找 到第一个非有效的字符为止，然后把该字符之前的字符串转换成数字。不过，对于这个方法来说，第一 个出现的小数点是有效字符。如果有两个小数点，第二个小数点将被看作无效的，`parseFloat()`方法会把 这个小数点之前的字符串转换成数字。

```javascript
console.log(parseFloat("1234blue"));  //return 1234
console.log(parseFloat("22.5"));  //return 22.5
console.log(parseFloat("22.34.5"));  //return 22.34
console.log(parseFloat("0908"));  //return 908
console.log(parseFloat("blue"));  //return NaN
```

#### 字符串

 几乎每个数对象都提供了`toString()`函数将内容转换为字符串形式。最为简单的转换为字符串的方 式，直接在任意数据后面 + '' 或 "" 即可。

```javascript
var data = 10;
console.log(data.toString());// "10"
data = true;
console.log(data.toString());// "true"
// toString()不能对null和undefined使用
data = null;
// 会报错Uncaught TypeError: Cannot read property 'toString' of null
// console.log(data.toString());
data = undefined;
// 会报错Uncaught TypeError: Cannot read property 'toString' of null
// console.log(data.toString());
// 拼接字符串可以对null和undefined使用
data = null + '';
console.log(data.toString());
data = undefined + "";
console.log(data.toString());
```

### 运算符

运算符用于执行程序代码运算，会针对一个及其以上操作数来进行运算。

#### 算数运算符

+、-、*、/、%、++、--

#### 赋值和扩展运算符

=、+=、-=、*=、/=、%=

#### 比较运算符 

==、===、!=、>、<、>=、<=

#### 逻辑运算符

&&、||、！

#### 三目运算符

```JavaScript
var a = 3;
var b = 5;
// 3大于5吗(返回true|false) ? 大于(true)返回a : 小于(false)返回b
var result = a > b ? a : b;
console.log(result);
```

### 控制语句

#### 选择执行

```javascript
if (条件表达式1) {
 语句体1;
} else if (条件表达式2) {
 语句体2;
} else if (条件表达式3) {
 语句体3；
}
 ...
[else {
 语句体n+1;
}]
```

#### 循环执行

```javascript
for (初始化语句; 判断条件语句; 控制条件语句) {
 循环体语句;
}
for (var i = 0; i < 10; i++) {
 console.log(i);
}
```

### 数组

数组（array）是按次序排列的一组数据，每个值的位置都有编号（从 0 开始），整个数组用方括号 表示。Js中定义数组的三种方式如下（也可先声明再赋值）：

```javascript
var arr = []; // 创建一个空数组
var arr = [值1, 值2, 值3];  // 创建一个数组并赋值
var arr = new Array(值1, 值2, 值3);  // 直接实例化
var arr = new Array(size);  // 创建数组并指定长度
```

数组中的每一个元素都可以被访问和修改，甚至是不存在的元素，无所谓越界。获取一个不存在的位置，不会报错越界，会返回undefined

**数组遍历**

```javascript
for (var i = 0; i < 数组.length; i++) {
 数组名[i]是获取元素
};
var arr = [1, '2', 3.3, true, null];
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

### 函数

方法1

```js
function 函数名([参数列表]){
    
}
// 声明函数
function foo1() {
    console.log('foo1');
}
// 调用函数
foo1();
```

方法2

```js
var 变量名 = function ([参数列表]) {
    
}
变量名();
// 声明函数
var foo2 = function () {
    console.log('foo2');
}
// 调用函数
foo2();
```

**return语句**

函数的执行可能会有返回值，需要使用return语句将结果返回。return语句不是必需的，如果没有的 话，该函数就不返回任何值，或者说返回undefined。 

作用： 

- 在没有返回值的方法中，用来结束方法。 
- 有返回值的方法中，一个是用来结束方法，一个是将值带给调用者。

## JavaScript内置对象

### String

charAt(idx)：返回指定位置处的字符。 

indexOf(Chr)：返回指定子字符串的位置，从左到右。找不到返回-1 

substr(m,n)：返回给定字符串中从m位置开始，取n个字符，如果参数n省略，则意味着取到字符串末 尾。 

substring(m,n)：返回给定字符串中从m位置开始，到n位置结束，不包含n位，如果参数n省略，则意味 着取到字符串末尾。 

toLowerCase()：将字符串中的字符全部转化成小写。 

toUpperCase()：将字符串中的字符全部转化成大写。 

replace(s1, s2)：替换，将s1替换为s2。 length: 属性，不是方法，返回字符串的长度。

```javascript
// charAt(idx)：返回指定位置处的字符
var msg = 'IT is very good!';
var result = msg.charAt(1); // T
console.log(result, result.length);
// indexOf(Chr)：返回指定子字符串的位置，从左到右。找不到返回-1
var result = msg.indexOf("very");// 6
console.log(result);
// substr(m, n)：返回给定字符串中从m位置开始，取n个字符，如果参数n省略，则意味着取到字符串末
尾。
result = msg.substr(1, 8); // T is ver
console.log(result, result.length);
// substring(m,n)：返回给定字符串中从m位置开始，到n位置结束，不包含n位，如果参数n省略，则意味
着取到字符串末尾。
result = msg.substring(1, 8); // T is ve
console.log(result, result.length);
// toLowerCase()：将字符串中的字符全部转化成小写。
result = msg.toLowerCase(); // it is very good!
console.log(result, result.length);
// toUpperCase()：将字符串中的字符全部转化成大写。
result = msg.toUpperCase(); // IT IS VERY GOOD!
console.log(result, result.length);
// replace(s1, s2)：将s1字符串替换为s2字符串
result = msg.replace('IT', 'it');
console.log(result, result.length);
```

### Math

Math.random()：生成随机数 

Math.ceil()：向上取整 

Math.floor()：向下取整 

Math.round()：四舍五入取整

```javascript
var num = Math.random(); // 生成大于0小于1的浮点数
console.log(num);
num = Math.ceil(3.11223); // 向上取整 4
console.log(num);
num = Math.floor(3.55667); // 向下取整 3
console.log(num);
num = Math.round(3.11223); // 四舍五入 3
console.log(num);
```

### Date

```javascript
// 获取日期时间
getFullYear()年, getMonth()月, getDate()日, getDay()周,
getHours()时,getMinutes()分,getSeconds()秒
// 设置日期时间
setFullYear(), setMonth(), ...
toLoacaleString()
```

```javascript
// 获取日期时间
var current_date = new Date(); // 创建一个日期对象
console.log(current_date);
current_date_time = current_date.getFullYear(); // 年
console.log(current_date_time);
current_date_time = current_date.getMonth() + 1; // 月，返回的是0~11
console.log(current_date_time);
current_date_time = current_date.getDay(); // 周
console.log(current_date_time);
current_date_time = current_date.getDate(); // 日
console.log(current_date_time);
current_date_time = current_date.getHours(); // 时
console.log(current_date_time);
current_date_time = current_date.getMinutes(); // 分
console.log(current_date_time);
current_date_time = current_date.getSeconds(); // 秒
console.log(current_date_time);
// 返回一个本地时间的字符串
currrent_date_time = current_date.toLocaleString();
console.log(currrent_date_time);
// 设置日期时间
current_date.setFullYear(2008);
current_date.setMonth(7);
current_date.setDate(8);
current_date.setHours(20);
current_date.setMinutes(8);
current_date.setSeconds(8);
console.log(current_date.toLocaleString());
```

## JavaScript操作BOM对象

ECMAScript是JavaScript的核心，但如果要在Web中使用JavaScript，那么BOM（浏览器对象模型） 则无疑才是真正的核心。BOM提供了很多对象，用于访问浏览器的功能，这些功能与任何的网页内容无 关。多年来，缺少事实上的规范导致BOM既有意思又有问题，因为浏览器厂商会按照各自的想法随意去 扩展它。于是，浏览器之间共有的对象就成为了事实上的标准。这些对象在浏览器中得以存在，很大程 度上是由于他们提供了与浏览器的互操作型。W3C为了把浏览器中JavaScript最基本的部分标准化，已经 将BOM的主要方面纳入了HTML5的规范当中。

### window对象

BOM的核心对象是window，它表示浏览器的一个实例。window对象有双重角色，它既是通过 JavaScript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象。这意味着在网页中定义的任 何一个对象、变量和函数，都以window作为其Global对象，因此有权访问parseInt()等方法。如果页面中 包含框架，则每个框架都拥有自己的window对象，并且保存在frames集合中。在frames集合中，可以通 过数值索引（从0开始，从左至右，从上到下）或者框架的名称来访问相应的window对象。

#### 系统对话框

```html
<div id="dv">this is a div</div>
<button onclick="test_alert();">消息框</button>
<button onclick="test_prompt();">输入框</button>
<button onclick="test_comfirm();">确认框</button>
<script type="text/javascript">
   // 消息框
    function test_alert() {
        alert('消息框！');
   }
    // 输入框
    function test_prompt() {
        var item = prompt('请输入年龄');  // item得到输入的值
        alert(item);
        alert(prompt('请输入年龄', 18));  // 将输入的值输出
   }
    /*
   确认框
   返回值：boolean（true|false）
     */
    function test_comfirm() {
        var result = confirm('真的要改吗？');
        if (result) {
            // DOM操作
            var ele = document.getElementById("dv");
            ele.style.color = "red";
            ele.innerHTML = "<span>div is red</span>";
       } else {
            alert("没事别瞎点");
       }
   }
</script>
```

#### 打开窗口

`window.open()` 方法既可以导航到一个特定的URL也可以用来打开一个新的窗口

```html
<input type="button" onclick='openBaidu();' />
<script type="text/javascript">
    function openBaidu() {
        window.open('http://www.baidu.com', '_blank');// 新窗口打开百度
        window.open("http://www.baidu.com", "_self");// 当前窗口打开百度
        // window.open(); // 空白窗口
   }
</script>
```

#### 时间函数

`setTimeout()` ：在指定的毫秒数后调用函数或计算表达式，只执行一次。 `setInterval()` ：在指定的毫秒数后不停的调用函数或计算表达式，多次执行。 通过返回的标识也可以 `clearTimeout()` ， `clearInterval()` 来清除指定函数的执行。

```html
<h1 id="h1"></h1>
<input type="button" value="停止显示时间" onclick='stopShow();' />
<script type="text/javascript">
    // 延迟3 秒后出现 alert
    /*
 function hello() {
 alert("对不起, 久等了！");
 }
 window.setTimeout("hello()", 3000);
 */
    // 不停的打印当前时间，当时间秒数为0时显示为红色
    function showTime() {
        // 拿到当前时间
        var date = new Date();
        var time = date.toLocaleString();
        // 拿到相应对象
        var h1 = document.getElementById('h1');
        h1.innerHTML = time;
        console.log(date.getSeconds());
        var sec = date.getSeconds();
        sec = sec % 10; // 对10取余
        // 根据需求添加样式
        if(0 == sec) { // 当时间的秒数变成0时，显示红色字体
            h1.innerHTML = '<span style="color:red">' + time + '</span>';
       }
   }
    /*
 * 定时操作
 * 第一个参数：执行的方法；
 * 第二个参数：定时，单位是毫秒
 */
    // 接收setInterval()返回的标识值
    var timeout = window.setInterval(showTime, 1000);
    // 停止操作
    function stopShow() {
        window.clearInterval(timeout); // 返回的标识值用来停止函数
   }
</script>
```

### location对象

```html
<input type="button" value="刷新" onclick="window.location.reload();" />
<input type="button" value="百度" onclick="openBaidu();" />
<script type="text/javascript">
    function openBaidu() {
        // 用新的文档替换当前文档
        window.location.href = "http://www.baidu.com";
   }
</script>
```

###  document对象

## JavaScript事件模型

### 事件类型

JavaScript可以处理的事件类型为：鼠标事件、键盘事件、HTML事件。

### 常用事件

onload ：当页面或图像加载完后立即触发 

onclick ：鼠标点击某个对象 

onblur ：元素失去焦点 

onfocus ：元素获得焦点 

onchange ：用户改变域的内容 

onmouseover ：鼠标移动到某个元素上 

onmouseout ：鼠标从某个元素上离开 

onkeyup ：某个键盘的键被松开 

onkeydown ：某个键盘的键被按下

```html
<!DOCTYPE html>
<html>
 <head>
 <meta charset="utf-8" />
 <title>常用事件</title>
 <style type="text/css">
 div {
 width: 300px;
 height: 200px;
 background: gray;
 margin-top: 100px;
 }
 </style>
 </head>
 <body onload="loadFunc();">
 <button type="button" onclick="clickFunc();">点击事件</button><br/>
 用户名：<input id="user_id" type="text" onblur="blurFunc();"
onfocus="focusFunc();" onkeydown="keydownFunc();" onkeyup="keyupFunc();" />
 <span id="user_span"></span>
 <br />

 爱好：
 <select onchange="changeFunc();">
 <option>---请选择---</option>
 <option>篮球</option>
 <option>足球</option>
 <option>乒乓球</option>
 </select>

 <div onclick="clickFunc();" onmouseover="moverFunc();"
onmouseout="moutFunc();">我是一个div</div>
 <script type="text/javascript">
 function loadFunc() {
 alert('浏览器加载时调用指定函数执行的代码');
 }
 // onload：当页面或图像加载完后立即触发
 /*
 window.onload = function() {
 alert('浏览器加载时调用指定函数执行的代码');
 }
 */
 // onclick：鼠标点击某个对象
 function clickFunc() {
 alert('点击事件触发的效果');
 }
 // onblur：元素失去焦点
 function blurFunc() {
 document.getElementById('user_span').innerHTML = '用户名不能为空';
 }
// onfocus：元素获得焦点
 function focusFunc() {
 document.getElementById('user_span').innerHTML = '用户名为4~10个字
符';
 }
 // onkeydown：某个键盘的键被按下
 function keydownFunc() {
                // m是77
 if(77 == event.keyCode) {
 document.getElementById('user_span').innerHTML = '不要骂人，消
息无效';
 }
 }
 // onkeyup：某个键盘的键被松开
 function keyupFunc() {
 console.log(event.keyCode);
 if(77 == event.keyCode) {
 document.getElementById('user_id').value = '';
 }
 }

 // onchange：用户改变域的内容
 function changeFunc() {
 document.getElementById('user_span').innerHTML = '爱好已改变';
 }

 // onmouseover：鼠标移动到某个元素上
 function moverFunc() {
 document.getElementById('user_span').innerHTML = '鼠标已移动至div';
 }
 // onmouseout：鼠标从某个元素上离开
 function moutFunc() {
 document.getElementById('user_span').innerHTML = '';
 }
 </script>
 </body>
</html>
```

### 事件处理程序

事件就是用户或浏览器自身执行的某种动作。例如click、load和mouseover都是事件的名字，而响 应某个事件的函数就叫做事件处理程序（或事件侦听器）。事件处理程序的名字以“on”开头，因此click 事件的事件处理程序就是onclick，为事件指定处理程序的方式有好几种。

#### HTML事件处理程序

```html
<input type="button" value="Press me" onclick="alert('thanks');" />
```

这样做有一些缺点，例如耦合度过高，还可能存在时差问题（当用户点击按钮时，处理函数还未加 载到，此时处理函数是单独写的一段js代码），而且在不同的浏览器上可能会有不同的效果。

#### DOM事件处理程序

通过JavaScript指定事件处理程序的传统方式，就是将一个函数赋值给一个事件处理程序属性。这 种方式被所有现代浏览器所支持。这种方式首先必须取得一个要操作的对象的引用，每个元素都有自己 的事件处理程序属性，这些属性通常全都小写，例如onclick，然后将这种属性的值设为一个函数，就可 以指定事件处理程序了。例如：

```html
<!DOCTYPE html>
<html>
 <head>
 <meta charset="UTF-8">
 <title>DOM事件处理程序</title>
 <style type="text/css">
 div {
 width: 300px;
 height: 200px;
 background: gray;
 margin-top: 100px;
 }
 </style>
 </head>
 <body>
 <button id="myBtn">按钮</button>
 <span id="user_span"></span>
 <div id="dv">我是一个div</div>
 <script type="text/javascript">
 var btn = document.getElementById('myBtn');
 btn.onclick = function() {
 alert('you click a button');
 }
 // onclick：鼠标点击某个对象
 function clickFunc() {
 alert('点击事件触发的效果');
 }
 // onmouseover：鼠标移动到某个元素上
 function moverFunc() {
 document.getElementById('user_span').innerHTML = '鼠标已移动至div';
 }
 // onmouseout：鼠标从某个元素上离开
 function moutFunc() {
document.getElementById('user_span').innerHTML = '';
 }
            // DOM方式处理 解耦
 var dv = document.getElementById('dv');
 dv.onclick = clickFunc;
 dv.onmouseover = moverFunc;
 dv.onmouseout = moutFunc;
 </script>
 </body>
</html>
```

!>也可以通过DOM删除指定的事件处理程序，只要将属性值设为null即可

## JavaScript操作DOM对象

### 什么是DOM

要实现页面的动态交互效果，BOM操作远远不够，需要操作 html 才是核心。如何操作 html，就是 DOM。简单的说，DOM提供了用程序动态控制 html 接口。DOM即文档对象模型描绘了一个层次化的节 点树，运行开发人员添加、移除和修改页面的某一部分。DOM处于javascript 的核心地位上。

每个载入浏览器的 HTML 文档都会成为 Document 对象。Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

![](https://box.kancloud.cn/a9d0a35ebc676b65f082c44a1e50904e_486x266.png)

### 节点

加载 HTML 页面时，Web 浏览器生成一个树型结构，用来表示页面内部结构。DOM 将这种树型结构 理解为由节点组成，组成一个节点树。对于页面中的元素，可以解析成以下几种类型的节点：

| 节点类型 | HTML内容         | 例如              |
| -------- | ---------------- | ----------------- |
| 文档节点 | 文档本身         | 整个文档 document |
| 元素节点 | 所有的HTML元素   | `<div>`           |
| 属性节点 | HTML元素内的属性 | id、name          |
| 文本节点 | 元素内的文本     | hello             |
| 注释节点 | HTML中的注释     | `<!---->`         |

### 元素节点的操作

当HTML文档在被解析为一颗DOM树以后，里面的每一个节点都可以看做是一个一个的对象，我们 成为DOM对象，对于这些对象，我们可以进行各式各样的操作，查找到某一个或者一类节点对象，可以 创建某种节点对象，可以在某个位置添加节点对象，甚至可以动态地删除节点对象，这些操作可以使我 们的页面看起来有动态的效果，后期结合事件使用，就能让我们的页面在特定时机、特定的事件下执行 特定的变换。

#### 获取节点

| 方法                     | 描述                                                |
| ------------------------ | --------------------------------------------------- |
| getElementById()         | 根据id获取==dom对象==，如果id重复，那么以第一个为准 |
| getElementsByTagName()   | 根据标签名获取==dom对象数组==                       |
| getElementsByClassName() | 根据样式名获取==dom对象数组==                       |
| getElementsByName()      | 根据name属性值获取==dom对象数组==，常用于多选获取值 |

#### 创建节点和插入节点

很多时候我们想要在某个位置插入一个新的节点，此时我们首先需要有一个节点存在，可以通过以 下几种方式创建新节点。

**创建节点**

**插入节点**

#### 间接查找节点

### 删除节点

第一种：获取父节点，然后删除子节点

 `父节点.removeChild(childNode);` 

第二种：通过旧节点定位到父节点，然后删除子节点 

`childNode.parentNode.removeChild(childNode);`

## 属性操作

在操作DOM对象时，除了可以操作对象整体之外，还可以更加灵活地操作对象中的各个属性。

| 方法\|属性         | 描述                         |
| ------------------ | ---------------------------- |
| getAttribute()     | 返回指定元素的属性值         |
| getAttributeNode() | 返回指定属性节点             |
| element.id         | 设置或者返回元素的 id        |
| setAttribute()     | 设置或者改变指定属性并指定值 |
| setAttributeNode() | 设置或者改变指定属性节点     |
| element.style      | 设置或返回元素的样式属性     |
| element.className  | 设置或返回元素的class属性    |
| element.classList  | 返回元素的类名               |

# jQuery

jQuery 是一套兼容多浏览器的 javascript 脚本库. 核心理念是写得更少，做得更多，使用 jQuery 将极大的提高编写 javascript 代码的效率,帮助开发者节省了大量的工作,让写出来的代码更加优雅, 更加 健壮，“如虎添翼”. 同时网络上丰富的 jQuery 插件也让我们的工作变成了"有了 jQuery,一切 soeasy."-- 因为我们已经站在巨人的肩膀上了。

**安装**

```html
<!-- 引入jQuery文件 -->
<script type="text/javascript" src="js/jquery-3.3.1.min.js" ></script>
```

## jQuery核心

`$` 符号在 jQuery 中代表对jQuery对象的引用， jQuery是核心对象，通过该对象可以获取jQuery对 象，调用jQuery提供的方法等。只有jQuery对象才能调用jQuery提供的方法。

## jQuery选择器

| 选择器       | 名称                | 举例                                                         |
| ------------ | ------------------- | ------------------------------------------------------------ |
| 元素选择器   | element             | `$("div")` 选择所有div元素 `$("div[id='mydiv']")` 选择 `id='mydiv'` 的div元素 |
| id选择器     | \#id                | `$("#dv")` 选择 `id="dv"` 的元素                             |
| 类选择器     | .class              | `$(".blue")` 选择所有 class="blue" 的元素 `$("span.blue")` 选择所有 class="blue" 的span元素 |
| 选择所有元素 | *                   | `$("*")` 选择页面所有元素                                    |
| 组合选择器   | e1, e2, eN          | `$("#dv, span, .blue")` 同时选中这几个选择器匹配的 元素      |
| 后代选择器   | ancestor descendant | `$("#parent div")` 选择 id="parent" 的元素的所有子 div元素   |

## jQuery操作DOM

jQuery也提供了对HTML节点的操作，而且在原生js的基础之上进行了优化，使用起来更加方便。 常用的从几个方面来操作，查找元素（选择器已经实现）；创建节点对象；访问和设置节点对象的 值，以及属性；添加节点；删除节点；删除、添加、修改、设定节点的CSS样式；动画操作等。注意： 以下的操作方式只适用于jQuery对象。

### 操作元素的属性

#### 遍历元素

`$(selector).each(function(index, element))` 遍历元素

- 参数 function 为遍历时的回调函数 
- index 为遍历元素的序列号，从 0 开始。
- element是当前的元素。

#### 获取属性

| 方法            | 描述                                 | 举例                         |
| --------------- | ------------------------------------ | ---------------------------- |
| attr(属性名称)  | attr(属性名称)                       | attr('checked') attr('name') |
| prop(属性名 称) | 获取具有true和false两个属性的属性 值 | prop('checked')              |

!>attr() ：操作 checkbox 时选中返回 checked，没有选中返回 undefined prop() ：可以获取元素名称 prop("tagName") ，获取 checkbox 建议使用 prop() ， attr() 无 法获取变化的checkbox，只可以获取静态的状态，而 prop() 都可以。

#### 设置属性

| 方法                    | 描述                                                         | 举例                                                |
| ----------------------- | ------------------------------------------------------------ | --------------------------------------------------- |
| attr(属性名称，属性值)  | 设置指定的属性值 attr(属性名称，属性值)                      | attr('checked', 'checked') attr('name', 'zhangsan') |
| prop(属性名 称，属性值) | 设置具有true和false两个 属性的属性值获取具有true和false两个属性的属性 值 | prop('checked', 'true')                             |

#### 移除属性

removeAttr(属性名)

#### 操作元素的样式

对于元素的样式，也是一种属性，由于样式用得特别多，所以对于样式除了当做属性处理外还可以 有专门的方法进行处理。

| 方法                    | 说明                          |
| ----------------------- | ----------------------------- |
| attr(“class”)           | 获取class属性的值，即样式名称 |
| attr(“class”, ”样式名”) | 修改class属性的值，修改样式   |
| addClass(“样式名”)      | 添加样式名称                  |
| css()                   | 添加具体的样式                |
| removeClass(class)      | 移除样式名称                  |

#### 操作元素的内容

对于元素还可以操作其中的内容，例如文本，值，甚至是html。

| 方法             | 说明                           |
| ---------------- | ------------------------------ |
| html()           | 获取元素的html内容             |
| html("html内容") | 设定元素的html内容             |
| text()           | 获取元素的文本内容，不包含html |
| text("text内容") | 设置元素的文本内容，不包含html |
| val()            | 获取元素value值                |
| val("值")        | 设定元素的value值              |

#### 创建元素

在jQuery中创建元素很简单，直接使用核心函数即可。

$('元素内容'); 

#### 添加元素

| 方法                           | 描述                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| $("body").prepend(content)     | 在被选元素内部的开头插入元素或内容，被追加的 content 参数，可以是字符、HTML 元素标记。 |
| $(content).prependTo(selector) | 把 content 元素或内容加入 selector 元素开头                  |
| $("body").append(content)      | 在被选元素内部的结尾插入元素或内容，被追加的 content 参数，可以是字符、HTML 元素标记。 |
| $(content).appendTo(selector)  | 把 content元素或内容插入selector 元素内，默认是在尾部        |

#### 删除元素

| 方法     | 描述                                                 |
| -------- | ---------------------------------------------------- |
| remove() | 删除所选元素或指定的子元素，包括整个标签和内容一起删 |
| empty()  | 清空所选元素的内容                                   |

## jQuery事件

### 加载事件

ready() 类似于 onload() 事件， ready() 可以写多个，按顺序执行。

```javascript
$(document).ready(function(){
    
});
等价于
$(function(){
    
});
等价于
window.onload = function() {
};

```

### 绑定事件

绑定事件可以使用三种方式来实现，分别是 bind() ， click具体的事件类型 ， on() ，下面就让我 们一起来学习一下三种绑定事件的方式。

```html
<html>
 <head>
 <meta charset="UTF-8">
 <title>jQuery绑定事件</title>
 </head>
 <body>
 <button id="btn" type="button">测试单个事件按钮</button>
 <script type="text/javascript" src="js/jquery-3.3.1.min.js" ></script>
 <script type="text/javascript">
 function show() {
 alert('我是一个警告框！');
 }
 // ---------------------绑定单个事件--------------------
 // js方式实现绑定事件
 document.getElementById('btn').onclick = show;
 document.getElementById('btn').onclick = function() {
 alert('不好意思我又来了！');
 }
 // jQuery方式实现绑定事件 第一种
 // 通过事件类型，对应函数
 $('#btn').bind('click', function() {
 alert('jQuery方式绑定事件！');
 });
 $('#btn').bind('click', show);
 // jQuery方式实现绑定事件 第二种
 // 通过具体的事件类型，对应函数
 $('#btn').click(function() {
 alert('jQuery方式绑定事件第二种方式！');
 });
 $('#btn').click(show);

 // jQuery方式实现绑定事件 第三种 推荐的方式
 // 利用事件代理，只在document上注册事件，内存占用小，绑定事件快。
 $('#btn').on('click', function() {
 alert('jQuery方式绑定事件第三种方式！');
 });

 $('#btn').on('click', show);
 </script>
 </body>
</html>

```

!>事件绑定推荐大家使用第三种，内存占用小，绑定事件快。