## 1. JavaScript 简介

JavaScript是一种运行在浏览器中的解释型的编程语言。JavaScript 能跨平台、跨浏览器驱动网页，与用户交互。在Node.js把 JavaScript引入到了服务器端后， JavaScript 变成了全能型选手。具体而言，你可以使用 JavaScript 语言开发 Web或移动应用、实时网络应用、命令行工具、游戏等。

下面是两句简单的 JavaScript 代码 ：

```javascript
// 打印 Hello World.
console.log('Hello World');

/*（多行注释）弹出提示*/
alert('温馨提示：不要长时间盯着屏幕，注意休息。');
```

JavaScript代码可以直接嵌在网页的任何地方。通常使用 JavaScript 代码有2种方法：

- 放到`<head>`中，将JavaScript代码包含`<script>...</script>`中，它将直接被浏览器执行。
- （推荐）把JavaScript代码放到一个单独的`.js`文件(如 `index.js`)，然后在HTML中通过`<script src="..."></script>`引入。这种方法有利于维护代码，且多个页面可以各自一用同一份`.js` 文件

```javascript
<html>
<head>
  <script src="/static/js/index.js"></script>
</head>
<body>
  ...
</body>
</html>
```

推荐的编辑器：[Visual Studio Code](https://code.visualstudio.com/)

代码调试：使用 Google Chrome 浏览器的“查看(View)”-“开发者(Developer)”-“开发者工具(Developer Tools)”。Mac 下可使用`⌥+⌘+J`打开console（控制台）。



## 2. JavaScript 基础

### 2.1 基本语法

- 每个语句以`;`结束。

- 语句块`{...}`是一组语句的集合。花括号`{...}`内的语句具有缩进，通常是4个空格。`{...}`还可以嵌套，形成层级结构。但应避免过多的嵌套，可以使用将代码写在函数里，再通过调用函数以减少代码的复杂度。
- 严格区分大小写。



### 2.2 数据类型和变量

#### Number（整数和浮点数）

以下是合法的 Number 类型，Number可以直接做四则运算，规则和数学一致。

```javascript
23; 			// 整数23
3.14; 		// 浮点数3.14
1.234e4; 	// 科学计数法表示1.234x10000，等同于1234
-42; 			// 负数
NaN; 			// 当无法计算结果时用NaN(Not a Number)表示
Infinity; // 当数值超过了JavaScript的Number所能表示的最大值时，表示为Infinity(无限大).
```

#### 字符串

字符串是以单引号`'`或双引号`"`中的任意文本。

#### 布尔值

一个布尔值只有`true`、`false`两种值，常用在条件判断中。你可以直接用`true`、`false`表示布尔值，也可以通过布尔运算计算出来。 

- JavaScript 中建议始终使用`===`比较。

#### null 和 undefined

`null`表示一个“空”的值，类似 Swift 的 `nil`。`undefined`表示“未定义”。两者区别不大，因此除了在判断函数参数是否传递的情况下用 `undefined`，其他情况一般用用`null`。



#### 变量

使用`var`申明的变量，其范围被限制在该变量被申明的函数体内，同名变量在不同的函数体内互不冲突。

使用等号`=`对变量进行赋值：可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量。这是因为 JavaScript 是一种动态类型的语言，很灵活。

关于变量名的规定：

- 大小写英文、数字、`$`和`_`的组合，且不能以数字开头。
- 不能是保留字（关键字），且应有意义。
- 不能包含空格或连字符，区分大小写。

```javascript
var name = 'John';
name = 23;
```



#### 数组

数组(Array)是一组按顺序排列的集合，集合的每个值称为元素。数组的元素可以通过索引来访问，索引的起始值为`0`。

```javascript
//	JavaScript的数组可以包括任意数据类型,建议使用下面的方法建立数组。
var myArray = [ ‘Hi’, 42, 3.14, true, null];
myArray[0];  //返回索引为0的元素，即Hi.
myArray[5];  //索引超出范围，返回undefined.

// 建立数组的第二种方法：通过Array()函数创建数组
new Array(42, 23, 3.14); 


```

#### 对象

JavaScript的对象(Object)是一组由键-值组成的无序集合 。

键都是字符串类型，又称对象的属性，通过`对象变量.属性名`（Dot Notation）的方式可以获取一个对象的属性。

而值可以是任意数据类型。

```javascript
var person = {
    name: 'John',
    age: 23,
    tags: ['iOS', 'Android', 'Web'],
    city: 'California'
};
```

