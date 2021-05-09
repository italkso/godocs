# JSON

## 1. JSON 是一种数据交换格式

- **JSON （JavaScript Object Notation）** 

  - 基于JavaScript 对象字面量**表示法**，使用 键 - 值对 表示数据，独立于编程语言。

  - 文件扩展名`.json`
  - 媒体类型（MIME 类型）是 `application/json`（[媒体类型列表](http://www.iana.org/assignments/media-types/media-types.xhtml)）

- **表示法**

  一个用于表示诸如数字或单词等数据的字符系统。

- **数据交换格式**

  一种在不同平台间传递数据的文本格式（ XML 和 JSON），数据交换格式的核心是数据。

- **可移植性**

  以一种对双方系统都兼容的方式在平台间传递信息，是一种数据交换格式所追求的一个重要指标。

  为了获得最大可移植性，应尽可能避免使用空格或特殊字符。
  
  

JSON 是一种数据交换格式，完成数据交换（数据的传递）；是存储数据的载体，比如基于 JSON 的 NoSQL 数据库；也可以作为配置文件，沟通人和计算机之间。当 JSON 作为配置文件放在某一个地方时，它还是在扮演着数据交换格式的角色。

从 JavaScript 对象到JSON，再到服务端的对象，数据跑了一圈。每一天，数据都在全世界各种系统中进进出出，它们的载体就是数据交换格式。在考虑使用什么数据交换格式时，数据的形式和交换数据的系统都应该被考虑到。由于多数系统都使用对象来为数据建模，所以JSON 作为数据交换格式非常流行。但 JSON 不总是最佳选择。

- 在服务端，对象可以被序列化为 JSON 格式的文本，并且通过反序列化变回对象。服务端代码可以请求JSON。
- JSON 也可以被看作一种文本格式，用作一种面向文档存储类型的数据库的文档。比如 CouchDB。该数据库同时提供了可用于HTTP Web API 的接口。HTTP Web API 是一个对诸如HTML 或JSON 文档等资源进行请求和响应的系统。这些文档使用URL 经由HTTP 请求。
- JavaScript 的 XmlHttpRequest 可以通过URL 请求 JSON 资源。为了在 JavaScript 代码中使用 JSON，要使用JavaScript的 `JSON.parse()` 函数先将它反序列化为JSON 对象。



1. 解决常见的安全问题

2. 使用 JSON Schema 验证 数据格式是否正确

3. 浏览器、Web API 和 JSON 之间的关系

4. 服务端如何请求和创建数据

5. 如何在 jQuery 及其他客户端框架中使用 JSON

6. 为何 Couch NoSQL 数据库使用 JSON 存储数据

   

## 2. JSON语法及一致性验证

### 构建一个对象的语法

```json
{
    "fruit":"apple",
    "color":"red"
}
```

| 语法  | 名称   | 作用                                                        |
| ----- | ------ | ----------------------------------------------------------- |
| `{ }` | 花括号 | 左花括号 `{` 表示开始读取对象，右花括号 `}`表示结束读取对象 |
| `[ ]` | 方括号 | 左方括号`[`表示开始读取数组，右方括号 `]` 表示结束读取数组  |
| `:`   | 冒号   | 在键-值对中分隔名称和值                                     |
| `,`   | 逗号   | 分隔对象中的键-值对，分隔数组中的值，一个新部分的开始       |





### JSON 中的数据类型

| 数据类型 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 对象     | **花括号** ( `{ }` ) 包裹的「键 - 值对的列表」，对象可以嵌套其他对象。 |
| 字符串   | **双引号** ( `“”`) 包裹，可以由任何Unicode 字符构成。<br />当字符串本身需要包含双引号，使用反斜线对字符串中的双引号进行转义。 |
| 数字     | 用于传递数据的信息片段，可以是整数、小数、负数或指数。       |
| 布尔值   | `true` 或 `false` （小写）                                   |
| `null`   | 一个表示空值的 `null` 值 （`null` 小写）                     |
| 数组     | 值的集合或列表，使用方括号（`[]`）包裹，用逗号分隔值。<br />值可以是字符串、数字、布尔值、对象或数组 |

- 键 - 值对

  使用双引号包裹键，值可以是字符串、数字、布尔值、null、对象或数组。

- 对象和数组的主要区别

  - 对象是键 - 值对构成的列表或集合，数组是值构成的列表或集合
  - 数组中所有的值应具有相同的数据类型

- 避免在JSON 中混合使用数据类型

  

#### 示例

- 嵌套对象

```json
{
    "person":{
        "name": "Johnson Smith",
        "height": 180,
        "head": {
            "hair": {
                "color": "light blond",
                "length": "short",
                "style": "A-line"
            },
         "eyes": "brown"
        }
    }
}
```

- 使用反斜线进行转义

```json
{
"hello": "When I say \"Hello\", please repeat the word after me."
}
```

```json
{
"story": "\\t Once upon a time, in a far away land \\n there lived a princess."
}
```

- 数字

```json
{
"widgetInventory": 289,
"sadSavingsAccount": 22.59,
"seattleLatitude": 47.606209,
"seattleLongitude": -122.332071,
"earthsMass": 5.97219e+24
}
```

- 布尔类型

```json
{
    "toastWithBreakfast": false,
	"breadWithLunch": true
}
```

- null 类型

  假设我选修了法语，法语分数是 87，但是没有选修日语。

```json
{
	"French": 87,
	"Japanese": null
}
```

- 数组

  假设冰箱里有 5 个苹果，被我中午吃掉了2 个。

```json
{
    "fruit": [
    	"apple",
        null,
        "apple",
        null,
        "apple"
    ]
}
```

大多数语言都不允许变量的类型随意改变。正常情况下，在声明变量时，也需要说明它们是整型、字符串还是对象。当声明一个数组时，也要声明所有容器中所保存的数据都应是什么类型，且之后不能随意修改。JSON 作为一种数据交换格式，为了避免解析出错，应避免混合使用数据类型。

```json
{
    "Languages": [
        "English",
        "French",
        "Japanese"
    ]
}
```

```json
{
	"scores": [
		94.5,
		69.6,
		60
	]
}
```

```json
{
    "answers": [
        true,
        false,
        false,
        true,
        true
    ]
}
```

```json
{
    "quiz": [
        {
            "question": "What is the color of the ocean?",
            "answer": "Blue"
        },
        {
           "question": "What is JSON?",
            "answer": "JavaScript Object Notation" 
        },
        {
            "question": "There is 9 planets in the solar system.",
            "answer": false
        }
    ]
}
```

```json
{
    "quiz": [
        [
            true,
            false,
            ture,
            false,
            false
        ],
        [
            true,
            true,
            ture,
            false,
            false
        ],
        [
            true,
            false,
            false,
            ture,
            false
        ]
    ]
}
```



###  使用 JSON Schema 验证数据格式的正确性

JSON 验证器只负责负责验证语法错误。验证一致性需要使用 JSON Schema。

**JSON Schema**

- 使用 JSON 书写，是数据交换中的一种虚拟“**合同**”，提供**一致性验证（conformity validation）** 。

- 是数据接收方的第一道防线，能够帮助数据发送方节约时间、保证数据正确性。

- 也可以被接收方用于传输的另一端，位于要接收的数据的第一行，以保证数据符合要求。

- 支持正则表达式（一种字符形式，比如电子邮件地址的格式）

- 支持枚举类型（一个包含所有可能值的列表）

  


 **JSON Schema 解决的三个问题**

- **值的数据类型是否正确**

  规定一个值是数字、字符串等类型。

- **是否包含所需要的数据**

  对于数据，总有一些属性（或字段）必须包含值，也有一些不用包含。

  方法是将必填字段`"required" 数组`中，未包含在该数组内的就是不是必填字段。

- **值的形式是不是我需要的**

  可以对某类型的格式提出更具体的要求，比如指定范围、最小值和最大值。

  

**使用 JSON Schema 进行一致性验证（conformity validation）的步骤**

- 验证数据与 Schema的一致性

- 创建好数据

- 通过互联网向接收方发送数据，并收到了成功响应

  

**使用 JSON 书写 JSON Schema**

```json
{
	"$schema": "http://json-schema.org/draft-04/schema#",
	"title": "Cat",
	"properties": {
		"name": {
			"type": "string",
			"minLength": 3,
			"maxLength": 20
		},
		"age": {
			"type": "number",
			"description": "Your cat's age in years.",
			"minimum": 0
		},
		"declawed": {
			"type": "boolean"
		},
		"description": {
			"type": "string"
		}
	},
	"required": [
		"name",
		"age",
		"declawed"
	]
}
```

符合 JSON Schema 要求的合法 JSON

```json
{
    "name": "Fluffy",
    "age": 2,
    "declawed": false
    "description": "Fluffy loves to sleep all day."
}
```



## 3. 安全使用 JSON

####  客户端和服务端的关系

互联网浏览器和服务器（网站）之间的关系类似客户和服务员之间的关系。

这一关系包含了大量的请求和响应。浏览器通过互联网将请求发送给服务器，服务器接着就会把对应的页面作为响应发送给浏览器，然后浏览器就会将页面在屏幕上渲染出来。

客户端就是发生在用户浏览器中的一切，而服务端则是发生在运行网站的服务器中的一切。

客户端收到的响应就是HTML、CSS 和JavaScript 代码。服务端代码是指一些服务端语言，如ASP.NET、Ruby on Rails 或 Java。



#### 使用 JSON 可能产生的安全问题

JSON 只是文本，真正会产生安全问题的是 JSON 的使用。

在使用JSON 时，常见的安全漏洞通常发生在 JavaScript 从服务器获取到一段 JSON 字符串并将其转化为 JavaScript 对象时。

在Web 中使用 JSON 时可能会遇到以下攻击：

- **跨站请求伪造CSRF （cross-site request forgery，读作sea-surf）- 利用信任机制进行攻击** 

  一种利用站点对用户浏览器信任而发起攻击的方式，即利用了用户浏览器和网站间的凭证。

  为了防范这种攻击，应将将数组作为一个值存入 JSON 对象，避免在 JSON 中使用顶级数组；同时应仅允许POST 请求获取数据。

- **注入攻击 - 向网站注入恶意代码**

  注入攻击包含许多种形式与格式，但是它们都是利用系统本身的漏洞来实现的。

  注入攻击则主要通过**向网站注入恶意代码**来实现。比如，**跨站脚本攻击（cross-site scripting，XSS）**。抵御注入攻击的关键是要**找出可能的注入点**，并加入一些额外的步骤来加以防范。



#### 定位 JSON 安全问题

- **将数组作为一个值存入 JSON 对象**

  不要使用顶级数组，顶级数组是合法的 JavaScript 脚本，它们可以用`<script>` 标签链接并使用。顶层数组是可能会被攻击者利用的漏洞，应该避免。如果将数组作为一个值存入 JSON 对象，使其成为非法的 JavaScript 代码，就不会被`<script>` 标签加载了。

- **仅允许使用 HTTP POST 方法请求**

  对于不想公开的资源，仅允许使用 HTTP POST 方法请求，而不是 GET 方法。GET 方法可以通过URL 来请求，甚至可以放在`<script>` 标签中。

  GET 和POST 是HTTP 提供的用于与服务器交换数据的两种方法。GET 用于请求数据，得到响应。POST 用于提交数据，得到响应。如果服务器端允许GET 请求，就可以直接通过浏览器或`<script>` 标签链接到它。但POST 则不可以直接被链接到。一旦不能使用`<script>` 标签，攻击者就会受到资源共享策略的限制。

  当然，这并不意味着通过 HTTP 进行的 JSON 数据交换都应通过 POST 来进行。对于是否允许 GET 方法请求页面或资源，应该考虑：该页面是否需要通过URL 或`<script>` 标签来加载？如果不需要，就禁用 GET 方法，以阻止他人通过URL 和`<script>` 标签获取数据。

- **仅使用 JSON.parse() 解析JSON 数据**

  只有首先将代表对象的文本转换成对象并装入内存中，才能对其进行操作、观察，并在程序逻辑中使用。你可以使用 JavaScript 的`eval()` 函数或 `JSON.parse()` 解析 JSON 数据。

  `eval()` 函数会获取一段字符串，并传入的字符串编译执行，这会让代码易被攻击。因为`eval()` 函数会将传入的字符串无差别地编译执行。如果从第三方服务器中获取的JSON 被替换为了恶意脚本，那么站点就会无辜地蒙冤，在访问者的浏览器中编译执行恶意代码。

  更好的做法是，使用更加安全的 `JSON.parse()` 来代替 `eval()`， `JSON.parse()` 仅会解析 JSON 而不执行脚本。
  
  
  
  ```javascript
var jsonString = '{"animal": "cat"}';
  var myObject = JSON.parse(jsonString);
alert(myObject.animal);
  ```

  

  在Web 开发中，跨浏览器兼容和安全同等重要。`JSON.parse()` 目前已经被全部主流浏览器的最新版本所支持。针对不支持该函数的老式浏览器，可以将这一错误捕获，并弹出形如“请升级你的浏览器至最新版本”的消息。
  
  允许在 JSON 中使用HTML 以及直接将值插入页面是很危险的。为了使消息中不包含 HTML，可以在客户端和服务端都增加认证，并且将消息中所有的HTML 字符进行转码，使之成为非法的 HTML。
  
  

顶层 JSON 数组 (避免使用)：

```json
[
    {
        "user": "johonson"
    },
    {
        "phone": "555-555-5555"
    }
]
```

将数组作为一个值存入JSON 对象（推荐使用）：

```json
{
    "info": [
        {
            "user": "johonson"
        },
        {
            "phone": "555-555-5555"
        }
	]
}
```



## 4. XMLHttpRequest 与 Web API

JavaScript 中的 XMLHttpRequest 与 Web API 之间的关系是一种简单的客户端与服务端的关系。

- **XMLHttpRequest - 在客户端发起请求（浏览器发送对某项资源的请求）**

  一种 JavaScript 对象，无需刷新页面即可从一个URL 获取数据，常用于AJAX 编程。XMLHttpRequest 不仅限于XML，还可以用它来请求 JSON 资源。

  客户端跨域的 XMLHttpRequest 需要服务端的支持来保证 JSON 资源请求成功。JSON 资源可以通过一个URL 来请求，在浏览器中使用的URL （通用资源标识符）通常指向HTML 资源。

  

  【例】创建了一个新的XMLHttpRequest 对象，并让它从OpenWeather-Map API 获取JSON 数据。

  ```javascript
  //	创建一个新的 XMLHttpRequest 对象
  var myXMLHttpRequest = new XMLHttpRequest();
  
  var url = "http://api.openweathermap.org/data/2.5/weather?lat=35&lon=139";
  
  myXMLHttpRequest.onreadystatechange = function() {
      if (myXMLHttpRequest.readyState === 4 && myXMLHttpRequest.status === 200) {
          //	JSON响应的反序列化
          var myObject = JSON.parse(myXMLHttpRequest.responseText);
          
          //	对象的序列化
  		var myJSON = JSON.stringify(myObject);
      }
  }
  //	建立请求并通过 HTTP 协议发送
  myXMLHttpRequest.open("GET", url, true);
  myXMLHttpRequest.send();
  ```

  JavaScript 对象具有属性（键 - 值对），属性的值可以是一个函数。因为 JavaScript 中的函数也是一类对象，是一等公民。对象是一类数据，因此它可以被赋值给一个变量（属性）、修改和传递。

  JSON 对象中不包含可执行的指令。由于JSON 是用于数据交换的，所以它只包含属性。而编程中典型的对象还会包含函数（或方法）。

  **XMLHttpRequest 对象所拥有的属性**

  `onreadystatechange`，`readyState`，`response`，`responseText`，`responseType`，`responseXML`，`status`，`statusText`，`timeout`，`ontimeout`，`upload`以及 `withCredentials`

  

  - **onreadystatechange**

    可以在代码中将一个函数赋值给它（`onreadystatechange` 的值应该是一个函数）

  - **readyState**

    | 状态码 | 含义       | 解释                                           |
    | ------ | ---------- | ---------------------------------------------- |
    | 0      | 未发送     | open() 函数还没有执行                          |
    | 1      | 已发送     | open() 函数已执行，但send() 函数还没有执行     |
    | 2      | 接收到头部 | send() 函数已执行且头部和状态码都可以获取      |
    | 3      | 解析中     | 头部已经收到，但响应体正在解析中               |
    | 4      | 完成       | 请求完成，包括响应头和响应体的内容都已经接收到 |

    使用 jQuery 可以简化XMLHttpRequest 。通过使用jQuery，可以通过更为简单的`getJSON()` 函数来请求JSON，并且通过`done()`、`fail()`、`always()` 等方式来处理各种状态。

  - **responseText**

    当请求成功时，该属性会包含作为文本的响应体（如请求的 JSON）

  - **status**

    返回 HTTP 状态码（如200 表示请求成功）

    

  **XMLHttpRequest 中可用的函数**

  - `open（method，url，async（可选），user（可选），password（可选））`: 初始化请求
  - `send()`

  

- **Web API - 在服务端返回响应**

  通过HTTP 与服务进行交互的一系列指令与标准，这些交互可以包括创建、读取、更新、删除（CRUD）等操作，且Web API 都会有一份说明，概述如何使用这些指令和标准。

  网站为人服务，Web API 为代码服务，它们都使用HTTP 协议。

  

- **超文本传输协议（HTTP）**

  万维网使用的交换数据的基本协议。

  

- **异步操作 - AJAX**

  发生在幕后的、不会中断主进程的操作。JavaScript 的异步操作中，Web 浏览器的显示进程是主进程。

  JavaScript 中的异步（后台）操作被称为AJAX（ Asynchronous JavaScript and XML，异步的 JavaScript 和 XML）。AJAX 同样可以用来描述异步的 JavaScript 和 JSON。

  

- **序列化与反序列化**

  | 序列化与反序列化 | 含义                           | JavaScript 函数    |
  | ---------------- | ------------------------------ | ------------------ |
  | 序列化           | 将对象转化为文本的操作         | `JSON.stringify()` |
  | 反序列化         | 将序列化的文本转化为对象的操作 | `JSON.parse()`     |



- **同源策略**

  出于**安全**的考虑，浏览器仅会**请求同一个域的脚本**。同源策略使得JavaScript 和JSON 资源进行客户端- 服务端交流时出现了一些困难。

  

- **跨域资源共享（cross-origin resource sharing，CORS）**

  通过设置响应头，即在响应头额外加上一些带有`Access-Control-Allow` 前缀的属性，使得跨域请求资源（如JSON 文档）可以成功。

  ```JavaScript
  //	定义证书是否可用
  Access-Control-Allow-Credentials:true
  
  //	定义哪些 HTTP 方法可用
  Access-Control-Allow-Methods:GET, POST
  
  //	允许哪些域名，星号（*）表示允许任意域名
  Access-Control-Allow-Origin:*
  ```

  使用 CORS 进行安全防护

  ```javascript
  Access-Control-Allow-Methods:POST
  Access-Control-Allow-Origin:http://www.somebank.com
  ```

  使用CORS 也会遇到一些问题，而且也不是所有的JSON 数据都是从标准的Web API 获取的。

- **JSON-P**

  JSON-P 指带有padding （内联）的JSON，内联即将JavaScript 加入JSON 文档。JSON-P 利用用`<script>` 标签，绕过同源策略的限制，以从不同域名的服务器上请求JSON。

  JSON-P 是 CORS的备选方案。当不能使用CORS 时，仍需要通过某种关系来实现http://domainone.com 与http://domaintwo.com 之间的交流。

  ```javascript
  getTheAnimal(
      {
      	"animal": "cat"
  	}
  );
  
  //	在JavaScript 中声明的函数
  function getTheAnimal(data) {
  	var myAnimal = data.animal; 	// will be "cat"
  }
  
  //	创建<script> 标签，并将其动态添加到 HTML 文档的<head>标签中
  var script = document.createElement("script");
  script.type = "text/javascript";
  script.src = "http://notarealdomain.com/animal.json";
  document.getElementsByTagName('head')[0].appendChild(script);
  
  //	通过 queryString 告知服务器函数的名字
  script.src = "http://notarealdomain.com/animal.
  json?callback=getThing";
  
  //	JSON-P 中动态命名的函数
  getThing(
      {
     		 "animal": "cat"
      }
  );
  ```



## 5. JSON 与客户端框架

### 概念

- **抽象化**

  将一个大问题转换为多个小问题，以便简化对复杂系统的处理。

  在面对复杂问题时，你可以借助抽象化工具，每次只需要思考问题的一部分。

  

- **框架**

  计算机中的**框架**（库或工具包）就是一种**抽象化**工具，是一层位于软件或编程语言之上的为开发者提供支持的结构。框架能让开发人员节约时间、专注于构建功能。

  比如，与单纯使用 JavaScript 操作DOM 比较，在实现相同功能的前提下，使用代码更少的  jQuery 框架可以节约开发时间。

  Vue、 React 和 Angular 是当前应用最广的三大前端框架。

  

-  **[jQuery](http://jquery.com/)**

   jQuery 是允许开发者专注于**操作DOM** 构建功能的抽象化工具。

  -  jQuery 提供了JSON 请求和解析功能
  -  jQuery 解决了跨浏览器兼容问题

  - **jQuery.parseJSON()**

    一个jQuery 的函数，它不仅会调用`JSON.parse()` 函数，还会兼容那些不支持 `JSON.parse()` 函数的老式浏览器，且通过验证字符来评估字符串，从而避免了可能的安全问题。

    `jQuery.parseJSON()`的实现：先尝试使用原生的`JSON.parse()` 函数，当浏览器不支持时使用和`eval()` 功能类似的`new Function()`。同时，它会对一些不合法的字符进行检测，如果发现其中有注入攻击的威胁，就会抛出错误。

  - **jQuery.getJSON()**

    `jquery.ajax()` 函数的简写形式，其中包含了将JSON 解析为 JavaScript 对象的功能。

    

- **模型- 视图- 控制器（MVC）- 应用架构模式**

  模型（数据），视图（展示），控制器（更新模型和视图）

  

- **[AngularJS](http://angularjs.org/)**

  AngularJS 是一个基于模型- 视图- 控制器（MVC）的框架，专注于创建单页应用的抽象化工具。AngularJS试图将DOM 操作和业务逻辑解耦，它充分利用了JavaScript 对象 和JSON 的优势。

  

  传统多页Web 应用的方式与用户在客户端和服务端产生的交互是紧密联系在一起的。用户输入或点击URL，以通过HTTP 向服务端请求资源。这种用户、客户端、服务端共同参与的Web 应用，每动一步都需要请求一个新的页面。

  

  单页Web 应用致力于在浏览器中实现为用户提供无缝交互的应用体验，就像查找百科全书一样。这绝大部
  分是通过 JavaScript 以及XMLHttpRequest 实现的。当用户仍在当前页面时，幕后的代码已经完成对资源的请求，用户从一个资源跳跃到另一个资源的操作将不再需要通过URL 或是指向URL 的链接来进行。

  

  **AngularJS MVC**

  - **JSON** 是模型（JavaScript 对象即数据模型）

  - **HTML** 是视图，且提供了与模型进行数据绑定的语法，数据绑定指借助一系列的占位符将数据“绑定”在页面上。

  - **控制器**是使用 AngularJS 语法来定义和操作与模型和视图间的交互的 JavaScript 文件

  HTTP 请求会在后台执行，同时数据模型的更新会自动触发HTML 模板的更新。不需要初始化请求；所有这些都会在后台进行。或者说，根据MVC 的概念，我所编写的JavaScript 代码不需要去改变DOM。更新数据模型会自动更新视图。

### jQuery 支持与JSON 交互

jQuery 框架通过缩减请求和解析JSON 的时间来缩短开发时间，从而对JSON 提供支持。

```javascript
//	一个在浏览器中显示为“My Button”的按钮
<button id="myButton">My Button</button>

//	用于隐藏“My Button”的JavaScript 代码；它不会在浏览器中显示
document.getElementById("myButton").style.display = "none";

//	用于隐藏“My Button”的jQuery 代码
$("#myButton").hide();

//	jQuery 用 jQuery.parseJSON 函数解析JSON 
var myAnimal = jQuery.parseJSON('{ "animal" : "cat" }');

//	使用jQuery 仅需几行代码即可完成对JSON 数据的请求
var url = "http://api.openweathermap.org/data/2.5/weather?lat=35&lon=139";
$.getJSON(url, function(data) {
	// 对天气数据执行一些操作
});
```



### 使用 AngularJS 创建单页应用

【例】需要将用户登录页面中的消息“Hello, stranger” 改为针对登录用户的问候语。

- 用户未登录时的HTML 消息:

```html
<h1 id="message">Hello, stranger!</h1>
```

- 用户登录后对消息进行修改的JavaScript 代码:

```javascript
if (signedIn) {
    var message = "Hello, " + userName + "!";
    document.getElementById("message").innerHTML = message;
}
```

- 使用AngularJS 属性和数据绑定语法的HTML 视图

  HTML 标签（`<body>` 和`<div>`） 上的"ng-app" 和"ng-controller" 属性设置了一个支持数据绑定的视图。，数据绑定就是指借助一系列的占位符将数据“绑定”在页面上。AngularJS 语法要求在数据的占位符的两边加上标识。这些标识由两个左花括号（`{{`）和两个右花括号（`}}`）组成，它们应包裹着占位符（userData.userName）。

```html
<body ng-app="myApp">
    <div id="wrapper" ng-controller="myAppController">
        <h1 id="message">Hello {{ userData.userName}}!</h1>
    </div>  
</body>
```

包含userData 对象的JavaScript 控制器将被添加到全局作用域中，这会允许视图（HTML）使用该对象进行数据绑定。

```javascript
angular.module('myApp', [])
	.controller('myAppController', function($scope) {
	$scope.userData = { userName : "Stranger" };
	if(signedIn)
    {
        $scope.userData = { userName : "Bob" };
    }
});
```

如何将保存在某个数据库中的数据放入单页应用的数据模型中是开发者要做的事。在AngularJS 数据模型中，可以使用 JSON 把数据库中的数据放到数据模型中，即通过HTTP 协议来请求JSON 数据，是一种客户端- 服务端的关系。AngularJS 通过其核心服务`$http` 来简化通过这一协议进行的数据模型进行的检索。

从OpenWeatherMap API 获取天气数据:

```javascript
angular.module('myApp', [])
	.controller('myAppController', function($scope, $http) {
    $http.get('http://api.openweathermap.org/data/2.5/weather?lat=35&lon=139').
	success(function(data, status, headers, config) {
		$scope.weatherData = data;
	});
});
```

从OpenWeatherMap API 返回的JSON 数据会被$http 反序列化。然后它将作为名为weatherData 的对象被添加到全局作用域，这样就能通过 HTML 视图的插值语法将其作为数据模型进行绑定了。

```html
<body ng-app="myApp">
	<div id="wrapper" ng-controller="myAppController">
		<div>
			{{ weatherData.weather[0].description }}
		</div>
	</div>
</body>
```





## 6. 使用 JSON 文档存储数据

### 概念

- **关系型数据库**

  使用表格、行和列来以结构化形式存储数据，即用表格来组织和关联数据，每个表格都会保存有一定意义的数据。

  在关系型数据库中，常常会存在表、列、行以及它们之间的关系，其中会用到主键和外键。

  使用结构化查询语言（structured query language，SQL）可以创建、操作和查询这类关系型数据库。使用SQL，可以在数据库多个表的行和列之间进行查询。

-  **NoSQL 数据库**

  不通过存储数据间的关系来存储的数据库。NoSQL 数据库有许多种，比如：

  - 键值对存储模型：将数据简化为键值对，比如将英语词典编入数据库用键值对存储比较合适。
  - 文档存储：基于文档的概念组织数据，比如 XML 文档、JSON 文档等。

- **CouchDB**

  - 面向文档的NoSQL 数据库存储类型

  - 使用 JSON 文档的形式来存储数据（存储和管理 JSON 文档）

  - 会在存储与获取数据的同时维护好数据的结构

  - 使用基于HTTP 的API 来获取作为JSON 文档资源的数据

  - 使用JavaScript 作为查询语言，且通过视图的map 和reduce 方法来跨API 获取数据

    

## 7. JSON 在服务端扮演的角色

- 客户端

  HTML、CSS、JavaScript

- **服务端**

  在服务端，可以通过将 JSON 反序列化为对象而运用在编程逻辑中，也可以将对象序列化为JSON 格式。JSON 同时被客户端和服务端较好地支持，使得它在Web 领域从诸多数据交换格式中脱颖而出。

  - PHP：用于创建动态Web 页面的服务端脚本语言。
  - ASP.NET：微软开发的服务端Web 框架。
  - Node.js：基于谷歌V8 引擎的服务端JavaScript。
  - Ruby on Rails：使用Ruby 编写的服务端Web 应用框架。
  - Java：一种面向对象编程语言。
  - Go



## 8. 使用 JSON 作为配置文件

Node.js 默认的JavaScript 包管理器 npm 使用 JSON 作为配置文件，文件名称为`package.json`。内容如下：

```json
{
    "name":"bobatron",
    "version":"1.0.0",
    "description": "The extraordinary library of Bob.",
	"main": "bob.js",
    "scripts": {
        "prepublish": "coffee -o lib/ -c src/bob.coffee"
    },
    "repository": {
		"type": "git",
		"url": "git://github.com/bobatron/bob.git"
     },
	"keywords": [
			"bob",
			"tron"
	],
    "author": "Bob Barker <bob.barker@fakemail.com> (http://bob.com/)",
	"license": "BSD-3-Clause",
	"bugs": {
	"url": "https://github.com/bobatron/issues"
	}
}
```



| 配置文件格式 | 可读性 | 表示复杂数据的能力 | 数据类型 | 解析 |
| ------------ | ------ | ------------------ | -------- | ---- |
| INI          | 最好   | 差                 |          |      |
| XML          | 一般   | 好                 | 无       |      |
| JSON         | 较好   | 好                 | 有       | 便利 |

使用INI 格式的某游戏配置文件（settings.ini）:

```INI
[general]
playIntro=false
mouseSensitivity=0.54

[display]
complexTextures=true
brightness=4.2
widgetsPerFrame=326
mode=windowed

[sound]
volume=1
effects=0.68
```

使用XML 格式的某游戏配置文件（settings.xml）:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<settings>
    <general>
        <playIntro>false</playIntro>
		<mouseSensitivity>0.54</mouseSensitivity>
    </general>
    <dispaly>
    	<complexTextures>true</complexTextures>
		<brightness>4.2</brightness>
		<widgetsPerFrame>326</widgetsPerFrame>
    </dispaly>   
    <sound>
        <volume>1</volume>
		<effects>0.68</effects>
    </sound>
</settings>
```

使用JSON 格式的某游戏配置文件（settings.json）:

```json
{
    "general": {
        "playInfro": false,
        "mouseSensitivity": 0.54
    },
    "display": {
        "complexTextures": true,
		"brightness": 4.2,
		"widgetsPerFrame": 326,
        "mode": "windowed"
    },
    "sound": {
        "volume": 1,
		"effects": 0.68
    },
}
```





## 链接

- **JSON 验证**

  语法验证（关注 JSON 格式）

  - JSON Formatter & Validator（https://jsonformatter.curiousconcept.com/）
  - JSON Editor Online（http://www.jsoneditoronline.org/）
  - JSONLint（http://jsonlint.com/）

  一致性验证（关注 JSON 独特数据结构）

  - JSON Schema 主页（http://json-schema.org/）
  - JSON Schema 验证规范（http://json-schema.org/latest/json-schema-validation.html）
  - JSON Schema Lint（http://jsonschemalint.com/draft4/）
  - JSON Schema Validator（http://www.jsonschemavalidator.net/）



- **框架**
  - jQuery（http://jquery.com/）- 为DOM 操作服务的抽象化工具
  - AngularJS（http://angularjs.org/）- 专注于创建单页应用的抽象化工具
- **NoSQL**
  - CouchDB（http://couchdb.apache.org/）- 使用JSON 文档存储数据的 NoSQL 数据库

- 补充材料（代码示例、练习等）
  - https://github.com/lindsaybassett/json

