# 了解Ajax

**Ajax** 的全称是 Asynchronous Javascript And XML（**异步 JavaScript 和 XML**）。

通俗的理解：在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是Ajax。

# **jQuery中的Ajax**

## **了解**jQuery中Ajax

浏览器中提供的 XMLHttpRequest 用法比较复杂，所以 jQuery 对 XMLHttpRequest 进行了封装，提供了一系列 Ajax 相关的函数，极大地降低了 Ajax 的使用难度。

jQuery 中发起 Ajax 请求最常用的三个方法如下：

- $.get()
- $.post()
- $.ajax()

### **$.get()**函数的语法

jQuery 中 $.get() 函数的功能单一，专门用来发起 get 请求，从而将服务器上的资源请求到客户端来进行使用。

$.get() 函数的语法如下：

```
$.get(url, [data], [callback])
```

![image-20230228131624568](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202302281316666.png)

### $.get()发起不带参数的请求

使用 $.get() 函数发起不带参数的请求时，直接提供请求的 URL 地址和请求成功之后的回调函数即可，示例代码如下：

```
$.get('http://www.liulongbin.top:3006/api/getbooks', function(res) {
    console.log(res) // 这里的 res 是服务器返回的数据
})
```

###  $.get()发起带参数的请求

使用 $.get() 函数发起带参数的请求时，示例代码如下：

```
$.get('http://www.liulongbin.top:3006/api/getbooks', { id: 1 }, function(res) {
    console.log(res)
})
```

### **$.post()**函数的语法

jQuery 中 $.post() 函数的功能单一，专门用来发起 post 请求，从而向服务器提交数据。

$.post() 函数的语法如下：

```
$.post(url, [data], [callback])
```

![image-20230228134735993](D:%5CWED%5C%E7%9F%A5%E8%AF%86%E7%82%B9%5CAjax%5C%E5%9B%BE%E7%89%87%5C202302281347040.png)

### $.post() 向服务器提交数据

使用 $post() 向服务器提交数据的示例代码如下：

```
$.post('http://www.liulongbin.top:3006/api/addbook', // 请求的URL地址
   { bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社' }, // 提交的数据
   function(res) { // 回调函数
      console.log(res);
   })
```

### $.ajax()**函数的语法**

相比于 $.get() 和 $.post() 函数，jQuery 中提供的 $.ajax() 函数，是一个功能比较综合的函数，它允许我们对 Ajax 请求进行更详细的配置。

$.ajax() 函数的基本语法如下：

```
$.ajax({
   type: '', // 请求的方式，例如 GET 或 POST
   url: '',  // 请求的 URL 地址
   data: { },// 这次请求要携带的数据
   success: function(res) { } // 请求成功之后的回调函数
});
```

**6.4** **使用** **$.ajax()** **发起** **GET** **请求**

使用 $.ajax() 发起 GET 请求时，只需要将 type 属性的值设置为 'GET' 即可：

```jQuery
$.ajax({
   type: 'GET', // 请求的方式
   url: 'http://www.liulongbin.top:3006/api/getbooks',  // 请求的 URL 地址
   data: { id: 1 },// 这次请求要携带的数据
   success: function(res) { // 请求成功之后的回调函数
       console.log(res)
   }
})
```

**6.4** **使用** **$.ajax()** **发起** **POST** **请求**

使用 $.ajax() 发起 POST 请求时，只需要将 type 属性的值设置为 'POST' 即可：

```
$.ajax({
   type: 'POST', // 请求的方式
   url: 'http://www.liulongbin.top:3006/api/addbook',  // 请求的 URL 地址
   data: { // 要提交给服务器的数据
      bookname: '水浒传',
      author: '施耐庵',
      publisher: '上海图书出版社'
    },
   success: function(res) { // 请求成功之后的回调函数
       console.log(res)
   }
});
```

# form表单的基本使用

## **1.3 <form>**标签的属性**

![image-20230302092732641](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202303020927745.png)

**1. action**

action 属性用来规定当提交表单时，**向何处发送表单数据**。

action 属性的值应该是后端提供的一个 URL 地址，这个 URL 地址专门负责接收表单提交过来的数据。

当 <form> 表单在未指定 action 属性值的情况下，action 的默认值为当前页面的 URL 地址。



**注意**：当提交表单后，页面会立即跳转到 action 属性指定的 URL 地址

**2. target**

target 属性用来规定**在何处打开** **action URL**。

它的可选值有5个，默认情况下，target 的值是 _self，表示在相同的框架中打开 action URL。

![image-20230302092936249](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202303020929290.png)

**3. method**

method 属性用来规定**以何种方式**把表单数据提交到 action URL。

它的可选值有两个，分别是 get 和 post。

默认情况下，method 的值为 get，表示通过URL地址的形式，把表单数据提交到 action URL。



**注意：**

get 方式适合用来提交少量的、简单的数据。

post 方式适合用来提交大量的、复杂的、或包含文件上传的数据。

在实际开发中，<form> 表单的 post 提交方式用的最多，很少用 get。例如登录、注册、添加数据等表单操作，都需要使用 post 方式来提交表单。

**4. enctype**

enctype 属性用来规定在**发送表单数据之前如何对数据进行编码**。

它的可选值有三个，默认情况下，enctype 的值为 application/x-www-form-urlencoded，表示在发送前编码所有的字符。

![image-20230302093143182](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202303020931217.png)

**注意：**

在涉及到**文件上传**的操作时，**必须**将 enctype 的值设置为 multipart/form-data

如果表单的提交不涉及到文件上传操作，则直接将 enctype 的值设置为 application/x-www-form-urlencoded 即可！

## **1.4** **表单的同步提交及缺点**

**1.** **什么是表单的同步提交**

通过点击 submit 按钮，触发表单提交的操作，从而使页面跳转到 action URL 的行为，叫做表单的同步提交。

**2.** **表单同步提交的缺点**

①<form>表单同步提交后，整个页面会发生跳转，**跳转到** **action URL** **所指向的地址**，用户体验很差。

②<form>表单同步提交后，**页面之前的状态和数据会丢失**。

**解决方案：** **表单只负责采集数据，** **Ajax** **负责将数据提交到服务器**。

## **2.2** **阻止表单默认提交行为**

当监听到表单的提交事件以后，可以调用事件对象的 **`event.preventDefault()`** 函数，来阻止表单的提交和页面的跳转，示例代码如下：

```
$('#form1').submit(function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})

$('#form1').on('submit', function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})

```

## **2.3** **快速获取表单中的数据**

**1. serialize()** **函数**

为了简化表单中数据的获取操作，jQuery 提供了 serialize() 函数，其语法格式如下：

```
$(selector).serialize()
//serialize() 函数的好处：可以一次性获取到表单中的所有的数据。
```

**2. serialize()****函数示例**

```
<form id="form1">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <button type="submit">提交</button>
</form>

$('#form1').serialize()
// 调用的结果：
// username=用户名的值&password=密码的值

```

注意：在使用 serialize() 函数快速获取表单数据时，<font color=red>**必须为每个表单元素添加** **name** **属性**！</font>

## // 快速清空表单内容

   $('#formAddCmt')[0].**reset**()

# **art-template** **模板引擎**

模板引擎，顾名思义，它可以根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面。

**4.3** **模板引擎的好处**

①减少了字符串的拼接操作

②使代码结构更清晰

③使代码更易于阅读与维护

http://aui.github.io/art-template/zh-cn/index.html

## **1.** **什么是标准语法**

art-template 提供了 **{{ }}** 这种语法格式，在 {{ }} 内可以进行**变量输出**，或**循环数组**等操作，这种 {{ }} 语法在 art-template 中被称为标准语法。



<script type="text/html"></script> // 默认为 text/javascript  里面代码均默认为 javascript 代码不会在页面显示。

### **2.** **标准语法** **-** **输出** **2.** **标准语法** **-** **输出**

```
{{value}}
{{obj.key}}
{{obj['key']}}
{{a ? b : c}}
{{a || b}}
{{a + b}}
```

在 {{ }} 语法中，可以进行变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出。

### **3.** **标准语法** **–** **原文输出** **3.** **标准语法** **–** **原文输出**

```
{{@ value }}

```

如果要输出的 value 值中，包含了 HTML 标签结构，则需要使用**原文输出**语法，才能保证 HTML 标签被正常渲染。

### **4.** **标准语法** **–** **条件输出**

如果要实现条件输出，则可以在 {{ }} 中使用 **if** … **else if** … **/if** 的方式，进行按需输出。

```
{{if value}} 按需输出的内容 {{/if}}

{{if v1}} 按需输出的内容 {{else if v2}} 按需输出的内容 {{/if}}

```

### **5.** **标准语法** **–** **循环输出**

如果要实现循环输出，则可以在 {{ }} 内，通过 each 语法循环数组，当前循环的索引使用 **$index** 进行访问，当前的循环项使用 **$value** 进行访问。

```
{{each arr}}
    {{$index}} {{$value}}
{{/each}}
```

### **6.** **标准语法** **–** **过滤器**

```
{{value | filterName}}
```

过滤器语法类似**管道操作符**，它的上一个输出作为下一个输入。

定义过滤器的基本语法如下：

```
template.defaults.imports.filterName = function(value){/*return处理的结果*/}
```

### **6.** **标准语法** **–** **过滤器**

```
<div>注册时间：{{regTime | dateFormat}}</div>
```

定义一个格式化时间的过滤器 dateFormat 如下：

```
 template.defaults.imports.dateFormat = function(date) {
    var y = date.getFullYear()
    var m = date.getMonth() + 1
    var d = date.getDate()

    return y + '-' + m + '-' + d // 注意，过滤器最后一定要 return 一个值
 }
```

过滤器一定有一个返回值。

# **6.1** **正则与字符串操作**

## **1.** **基本语法**

exec() 函数用于检索字符串中的正则表达式的匹配。

如果字符串中有匹配的值，则返回该匹配值，否则返回 null。

```
RegExpObject.exec(string)
---------------------------------------------------------------
var str = 'hello'
var pattern = /o/
// 输出的结果["o", index: 4, input: "hello", groups: undefined]
console.log(pattern.exec(str)) 

```

## **2.** **分组**

正则表达式中 ( ) 包起来的内容表示一个分组，可以通过分组来**提取自己想要的内容**，示例代码如下：

```
 var str = '<div>我是{{name}}</div>'
 var pattern = /{{([a-zA-Z]+)}}/

 var patternResult = pattern.exec(str)
 console.log(patternResult)
 // 得到 name 相关的分组信息
 // ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]

```

## **3.** **字符串的** **replace** **函数**

replace() 函数用于在字符串中用一些字符**替换**另一些字符，语法格式如下：

```
var result = '123456'.replace('123', 'abc') // 得到的 result 的值为字符串 'abc456'
```

示例代码如下：

```
var str = '<div>我是{{name}}</div>'
var pattern = /{{([a-zA-Z]+)}}/

var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1]) // replace 函数返回值为替换后的新字符串。。。。patternResult是正则表达后获得的数组
// 输出的内容是：<div>我是name</div>
console.log(str)
```

**patternResult是正则表达后获得的数组** 和 pattern 不一样

## **4.** **多次** **replace**

```
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/
// \s*   \s*   表示空格   s必需要小写
var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1]) 
console.log(str) // 输出 <div>name今年{{ age }}岁了</div>

patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1])
console.log(str) // 输出 <div>name今年age岁了</div>

patternResult = pattern.exec(str)
console.log(patternResult) // 输出 null
```

## **5.** **使用** **while** **循环** **replace**

```
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while(patternResult = pattern.exec(str)) {
   str = str.replace(patternResult[0], patternResult[1])
}
console.log(str) // 输出 <div>name今年age岁了</div>
```

## **6. replace** **替换为真值**

```ajax
var data = { name: '张三', age: 20 }
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while ((patternResult = pattern.exec(str))) {
   str = str.replace(patternResult[0], data[patternResult[1]])
}
console.log(str)  // <div>张三今年20岁了</div>
```

# **6.2** **实现简易的自定义模板引擎**

**1.** **实现步骤**

①定义模板结构

②预调用模板引擎

③封装 template 函数

④导入并使用自定义的模板引擎

**2.** **定义模板结构**

```
<!-- 定义模板结构 -->
<script type="text/html" id="tpl-user">
   <div>姓名：{{name}}</div>
   <div>年龄：{{ age }}</div>
   <div>性别：{{  gender}}</div>
   <div>住址：{{address  }}</div>
</script>
```

**3.** **预调用模板引擎**

```
<script>
   // 定义数据
   var data = { name: 'zs', age: 28, gender: '男', address: '北京顺义马坡' }
   // 调用模板函数
   var htmlStr = template('tpl-user', data)
   // 渲染HTML结构
   document.getElementById('user-box').innerHTML = htmlStr
</script>

```

**4.** **封装** **template** **函数**

```
function template(id, data) {
  var str = document.getElementById(id).innerHTML
  var pattern = /{{\s*([a-zA-Z]+)\s*}}/
  var pattResult = null
  while ((pattResult = pattern.exec(str))) {
    str = str.replace(pattResult[0], data[pattResult[1]])
  }
   return str
}

```

**5.** **导入并使用自定义的模板引擎**

```
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>自定义模板引擎</title>
    <!-- 导入自定义的模板引擎 -->
    <script src="./js/template.js"></script>
</head>
```

\-----------------------------------------------------------------------------\----------------------------------------------------------------





-----------\-----------------------------------------------------------------------------\-------------------------------------------------------

# Ajax 加强



# XMLHttpRequest的基本使用

## **1.1** **什么** **XMLHttpRequest**

XMLHttpRequest（简称 xhr）是浏览器提供的 Javascript 对象，通过它，可以**请求服务器上的数据资源**。之前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的。

![s](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202303051400419.png)

## XMLHttpRequest 对象属性描述(用于和服务器交换数据。)_

![image-20230306181404804](https://wh22wxy-1314518111.cos.ap-chongqing.myqcloud.com/202303061814928.png)

## **1.2** **使用** **xhr** **发起** **GET** **请求**

①创建 xhr 对象

②调用 xhr.open() 函数

③调用 xhr.send() 函数

④监听 xhr.onreadystatechange 事件

```
// 1. 创建 XHR 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open 函数，指定 请求方式 与 URL地址
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
// 3. 调用 send 函数，发起 Ajax 请求
xhr.send()
// 4. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    // 4.1 监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

**if (xhr.readyState === 4 && xhr.status === 200) {}** 是判断服务器响应的固定判断格式。

## **1.3** **了解** **xhr** **对象的** **readyState** **属性**

XMLHttpRequest 对象的 readyState 属性，用来表示**当前** **Ajax** **请求所处的状态**。每个 Ajax 请求必然处于以下状态中的一个：

| 值                         | **状态**                          | **描述**                                                     |
| -------------------------- | --------------------------------- | ------------------------------------------------------------ |
| 0                          | UNSENT                            | XMLHttpRequest 对象已被创建，但尚未调用 open方法。           |
| 1                          | OPENED                            | open() 方法已经被调用。                                      |
| 2                          | HEADERS_RECEIVED                  | send() 方法已经被调用，响应头也已经被接收。                  |
| 3                          | LOADING                           | 数据接收中，此时 response 属性中已经包含部分数据。           |
| <font color='red'>4</font> | **<font color='red'>DONE</font>** | <font color='red'>Ajax 请求完成，这意味着数据传输已经彻底完成或失败。</font> |

**1.4** **使用** **xhr** **发起带参数的** **GET** **请求**

使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open 期间，为 URL 地址指定参数即可：

```
// ...省略不必要的代码
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=1')
// ...省略不必要的代码

```

这种在 URL 地址后面拼接的参数，叫做**查询字符串**。

## **1.5** **查询字符串**

定义：查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量）。

格式：将英文的 **?** 放在URL 的末尾，然后再加上 **参数＝值** ，想加上多个参数的话，使用 **&** 符号进行分隔。以这个形式，可以将想要发送给服务器的数据添加到 URL 中。

```
// 不带参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks
// 带一个参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks?id=1
// 带两个参数的 URL 地址
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记

```

## **2. GET** **请求携带参数的本质**

无论使用 $.ajax()，还是使用 $.get()，又或者直接使用 xhr 对象发起 GET 请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的。

```
$.get('url', { name: 'zs', age: 20 }, function () { })
        // 等价于
        $.get('url?name=zs&age=20', function () { })

        $.ajax({ method: 'GET', url: 'url', data: { name: 'zs', age: 20 }, success: function () { } })
        // 等价于
        $.ajax({ method: 'GET', url: 'url?name=zs&age=20', success: function () { } })

```

# **1.6 URL****编码与解码**

**1.** **什么是** **URL** **编码**

URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。

如果 URL 中需要包含中文这样的字符，则必须对中文字符进行**编码**（转义）。

**URL****编码的原则**：使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。

URL编码原则的通俗理解：使用英文字符去表示非英文字符。

```
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
// 经过 URL 编码之后，URL地址变成了如下格式：
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=%E8%A5%BF%E6%B8%B8%E8%AE%B0
```

浏览器提供了 URL 编码与解码的 API，分别是：

**`lencodeURI() `**编码的函数

**`ldecodeURI()`** 解码的函数

```
encodeURI('黑马程序员')
// 输出字符串  %E9%BB%91%E9%A9%AC%E7%A8%8B%E5%BA%8F%E5%91%98
decodeURI('%E9%BB%91%E9%A9%AC')
// 输出字符串  黑马
```

# **1.7** **使用** **xhr** **发起** **POST** **请求**

①创建 xhr 对象

②调用 xhr.open() 函数

③**设置** **Content-Type** **属性**（固定写法）

④调用 xhr.send() 函数，**同时指定要发送的数据**

⑤监听 xhr.onreadystatechange 事件

```
// 1. 创建 xhr 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open()
xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')

// 3. 设置 Content-Type 属性（固定写法）
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')

// 4. 调用 send()，同时将数据以查询字符串的形式，提交给服务器
xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')
// 5. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText)
    }
}
```

# **2.** **数据交换格式**

## **2.1** **什么是数据交换格式**

数据交换格式，就是服务器端与客户端之间进行数据传输与交换的格式。

前端领域，经常提及的两种数据交换格式分别是 XML 和 JSON。其中 XML 用的非常少，

### **2. XML** **和** **HTML** **的区别**

XML 和 HTML 虽然都是标记语言，但是，它们两者之间没有任何的关系。

- HTML 被设计用来描述网页上的**内容**，是网页内容的载体
- XML 被设计用来**传输和存储数据**，是数据的载体

## **3. XML****的缺点**

①XML 格式臃肿，和数据无关的代码多，体积大，传输效率低

②在 Javascript 中解析 XML 比较麻烦

```
<note>
  <to>ls</to>
  <from>zs</from>
  <heading>通知</heading>
  <body>晚上开会</body>
</note>
```

## **2.3 JSON**

### **1.** **什么是** **JSON**

概念：JSON 的英文全称是 JavaScript Object Notation，即“JavaScript 对象表示法”。简单来讲，JSON 就是 Javascript **对象和数组的字符串表示法**，它使用文本表示一个 JS 对象或数组的信息，因此，**JSON** **的本质是字符串**。

作用：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但是 JSON 比 XML 更小、更快、更易解析。

现状：JSON 是在 2001 年开始被推广和使用的数据格式，到现今为止，JSON 已经成为了主流的数据交换格式。

### **2. JSON** **的两种结构**

JSON 就是用字符串来表示 Javascript 的对象和数组。所以，JSON 中包含**对象**和**数组**两种结构，通过这两种结构的**相互嵌套**，可以表示各种复杂的数据结构。

1. **对象结构**：对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型。
2. **数组结构**：数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型。

### **3. JSON****语法注意事项**

①属性名必须使用双引号包裹

②字符串类型的值必须使用双引号包裹

③JSON 中不允许使用单引号表示字符串

④JSON 中不能写注释

⑤JSON 的最外层必须是对象或数组格式

⑥不能使用 undefined 或函数作为 JSON 的值

**JSON 的作用：在计算机与网络之间存储和传输数据。**

**JSON 的本质：用字符串来表示 Javascript 对象数据或数组数据**

### **4. JSON** **和** **JS**  **对象的关系**

JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。例如：

```
//这是一个对象
var obj = {a: 'Hello', b: 'World'}

//这是一个 JSON 字符串，本质是一个字符串
var json = '{"a": "Hello", "b": "World"}' 
```

### **5. JSON** **和** **JS** **对象的互转**

要实现从 JSON 字符串转换为 JS 对象，使用 **`JSON.parse()`** 方法：

```
var obj = JSON.parse('{"a": "Hello", "b": "World"}')
//结果是 {a: 'Hello', b: 'World'}

```

要实现从 JS 对象转换为 JSON 字符串，使用 **`JSON.stringify()`** 方法：

```
var json = JSON.stringify({a: 'Hello', b: 'World'})
//结果是 '{"a": "Hello", "b": "World"}'
```

### **6.** **序列化和反序列化**

把**数据对象**转换为**字符串**的过程，叫做**序列化**，例如：调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。

把**字符串**转换为**数据对象**的过程，叫做**反序列化**，例如：调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

# **3.** **封装自己的** **Ajax** **函数**

## **3.2** **定义** **options** **参数选项**

itheima() 函数是我们自定义的 Ajax 函数，它接收一个配置对象作为参数，配置对象中可以配置如下属性：

- method  请求的类型
- url      请求的 URL 地址
- data    请求携带的数据
- success  请求成功之后的回调函数

## **3.3** **处理** **data** **参数**

需要把 data 对象，转化成查询字符串的格式，从而提交给服务器，因此提前定义 resolveData 函数如下：

```
/**
 * 处理 data 参数
 * @param {data} 需要发送到服务器的数据
 * @returns {string} 返回拼接好的查询字符串 name=zs&age=10
 */
function resolveData(data) {
  var arr = []
  for (var k in data) {
    arr.push(k + '=' + data[k])
  }
  return arr.join('&')
}
```

## **3.4** **定义** **itheima** **函数**

在 itheima() 函数中，需要创建 xhr 对象，并监听 onreadystatechange 事件：

```
function itheima(options) {
  var xhr = new XMLHttpRequest()
  // 拼接查询字符串
  var qs = resolveData(options.data)

  // 监听请求状态改变的事件
  xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var result = JSON.parse(xhr.responseText)
      options.success(result)
    }
  }
}
```

## **3.5** **判断请求的类型**

不同的请求类型，对应 xhr 对象的不同操作，因此需要对请求类型进行 if … else … 的判断：

```
  if (options.method.toUpperCase() === 'GET') {
    // 发起 GET 请求
    xhr.open(options.method, options.url + '?' + qs)
    xhr.send()
  } else if (options.method.toUpperCase() === 'POST') {// toUpperCase()转换为大写
    // 发起 POST 请求
    xhr.open(options.method, options.url)
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    xhr.send(qs)
  }
```

# **4.1** **认识** **XMLHttpRequest Level2**

## **1.** **旧版** **XMLHttpRequest** **的缺点**

①只支持文本数据的传输，无法用来读取和上传文件

②传送和接收数据时，没有进度信息，只能提示有没有完成

## **2. XMLHttpRequest** **Level2** **的新功能**

①可以设置 HTTP 请求的时限

②可以使用 FormData 对象管理表单数据

③可以上传文件

④可以获得数据传输的进度信息

## **4.2** **设置** **HTTP** **请求时限**

有时，Ajax 操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。新版本的 XMLHttpRequest 对象，增加了 timeout 属性，可以设置 HTTP 请求的时限：

 **`xhr.timeout = 3000`**

上面的语句，将最长等待时间设为 3000 毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个 timeout 事件，用来指定回调函数：

```
 xhr.ontimeout = function(event){
     alert('请求超时！')
 }
```

## **4.3 FormData** **对象管理表单数据**

 Ajax 操作往往用来提交表单数据。为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：

```
      // 1. 新建 FormData 对象
      var fd = new FormData()
      // 2. 为 FormData 添加表单项
      fd.append('uname', 'zs')
      fd.append('upwd', '123456')
      // 3. 创建 XHR 对象
      var xhr = new XMLHttpRequest()
      // 4. 指定请求类型与URL地址
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      // 5. 直接提交 FormData 对象，这与提交网页表单的效果，完全一样
      xhr.send(fd)

```

FormData对象也可以用来获取网页表单的值，示例代码如下：

```
 // 获取表单元素
 var form = document.querySelector('#form1')
 // 监听表单元素的 submit 事件
 form.addEventListener('submit', function(e) {
    e.preventDefault()
     // 根据 form 表单创建 FormData 对象，会自动将表单数据填充到 FormData 对象中
     var fd = new FormData(form)
     var xhr = new XMLHttpRequest()
     xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
     xhr.send(fd)
     xhr.onreadystatechange = function() {}
})

```

## **4.4** **上传文件**

新版 XMLHttpRequest 对象，不仅可以发送文本信息，还可以上传文件。

实现步骤：

①定义 UI 结构

②验证是否选择了文件

③向 FormData 中追加文件

④使用 xhr 发起上传文件的请求

⑤监听 onreadystatechange 事件

### **1.** **定义** **UI** **结构**

```
    <!-- 1. 文件选择框 -->
    <input type="file" id="file1" />
    <!-- 2. 上传按钮 -->
    <button id="btnUpload">上传文件</button>
    <br />
    <!-- 3. 显示上传到服务器上的图片 -->
    <img src="" alt="" id="img" width="800" />

```

### **2.** **验证是否选择了文件**

```
 // 1. 获取上传文件的按钮
 var btnUpload = document.querySelector('#btnUpload')
 // 2. 为按钮添加 click 事件监听
 btnUpload.addEventListener('click', function() {
     // 3. 获取到选择的文件列表
     var files = document.querySelector('#file1').files
     if (files.length <= 0) {
         return alert('请选择要上传的文件！')
     }
     // ...后续业务逻辑
 })
```

### **3.** **向****FormData****中追加文件**

```
   
 // 1. 创建 FormData 对象
 var fd = new FormData()
 // 2. 向 FormData 中追加文件
 fd.append('avatar', files[0])
```

### **4.** **使用** **xhr** **发起上传文件的请求**

```
   
 // 1. 创建 xhr 对象
 var xhr = new XMLHttpRequest()
 // 2. 调用 open 函数，指定请求类型与URL地址。其中，请求类型必须为 POST
 xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar')
 // 3. 发起请求
 xhr.send(fd)
```

### **5.** **监听****onreadystatechange****事件**

```
   
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var data = JSON.parse(xhr.responseText)
    if (data.status === 200) { // 上传文件成功
      // 将服务器返回的图片地址，设置为 <img> 标签的 src 属性
      document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
    } else { // 上传文件失败
      console.log(data.message)
    }
  }
}
```

## **4.5** **显示文件上传进度**

新版本的 XMLHttpRequest 对象中，可以通过监听 xhr.upload.onprogress 事件，来获取到文件的上传进度。语法格式如下：

```
 // 创建 XHR 对象
 var xhr = new XMLHttpRequest()
 // 监听 xhr.upload 的 onprogress 事件
 xhr.upload.onprogress = function(e) {
    // e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算的长度
    if (e.lengthComputable) {
        // e.loaded 已传输的字节
        // e.total  需传输的总字节
        var percentComplete = Math.ceil((e.loaded / e.total) * 100)
    }
 }
 // 创建 XHR 对象
 var xhr = new XMLHttpRequest()
 // 监听 xhr.upload 的 onprogress 事件
 xhr.upload.onprogress = function(e) {
    // e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算的长度
    if (e.lengthComputable) {
        // e.loaded 已传输的字节
        // e.total  需传输的总字节
        var percentComplete = Math.ceil((e.loaded / e.total) * 100)
    }
 }

```

### **1.** **导入需要的库**

```
   
    <link rel="stylesheet" href="./lib/bootstrap.css" />
    <script src="./lib/jquery.js"></script>
```

### **2.** **基于** **Bootstrap** **渲染进度条**

```
   
    <!-- 进度条 -->
    <div class="progress" style="width: 500px; margin: 10px 0;">
      <div class="progress-bar progress-bar-info progress-bar-striped active" id="percent" style="width: 0%">
        0%
      </div>
    </div>
```

### **3.** **监听上传进度的事件**

```
   
 xhr.upload.onprogress = function(e) {
    if (e.lengthComputable) {
    // 1. 计算出当前上传进度的百分比
    var percentComplete = Math.ceil((e.loaded / e.total) * 100)
    $('#percent')
        // 2. 设置进度条的宽度
        .attr('style', 'width:' + percentComplete + '%')
        // 3. 显示当前的上传进度百分比
        .html(percentComplete + '%')
    }
 }
```

### **4.** **监听上传完成的事件**

```
   
 xhr.upload.onload = function() {
     $('#percent')
         // 移除上传中的类样式
         .removeClass()
         // 添加上传完成的类样式
         .addClass('progress-bar progress-bar-success')
 }
```

## **5.1 jQuery****实现文件上传**

**1.** **定义****UI****结构**

```
   
    <!-- 导入 jQuery -->
    <script src="./lib/jquery.js"></script>

    <!-- 文件选择框 -->
    <input type="file" id="file1" />
    <!-- 上传文件按钮 -->
    <button id="btnUpload">上传</button>
```

**2.** **验证是否选择了文件**

```
   
 $('#btnUpload').on('click', function() {
     // 1. 将 jQuery 对象转化为 DOM 对象，并获取选中的文件列表
     var files = $('#file1')[0].files
     // 2. 判断是否选择了文件
     if (files.length <= 0) {
         return alert('请选择图片后再上传！‘)
     }
 })
```

**3.** **向****FormData****中追加文件**

```
 // 向 FormData 中追加文件
 var fd = new FormData()
 fd.append('avatar', files[0])
```

**4.** **使用****jQuery****发起上传文件的请求**

```
 $.ajax({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/upload/avatar',
     data: fd,
     // 不修改 Content-Type 属性，使用 FormData 默认的 Content-Type 值
     contentType: false,
     // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器
     processData: false,
     success: function(res) {
         console.log(res)
     }
 })
```

**<font color='red'>// 不修改 Content-Type 属性，使用 FormData 默认的 `Content-Type` 值 `contentType: false`,
     // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器 `processData: false,`</font>**

## **5.2 jQuery** **实现** **loading** **效果**

**1. `ajaxStart(callback)`**

Ajax 请求**开始**时，执行 `ajaxStart `函数。可以在 ajaxStart 的 callback 中显示 loading 效果，示例代码如下：

```
    // 自 jQuery 版本 1.8 起，该方法只能被附加到文档
 $(document).ajaxStart(function() {
     $('#loading').show()
 })
注意： $(document).ajaxStart() 函数会监听当前文档内所有的 Ajax 请求。
```

**2. `ajaxStop(callback)`**

Ajax 请求**结束**时，执行 `ajaxStop`函数。可以在 ajaxStop 的 callback 中隐藏 loading 效果，示例代码如下：

```
  // 自 jQuery 版本 1.8 起，该方法只能被附加到文档
 $(document).ajaxStop(function() {
     $('#loading').hide()
 })
```

# **6. axios**

## **6.1** **什么是****axios**

Axios 是专注于**网络数据请求**的库。

相比于原生的 XMLHttpRequest 对象，axios **简单易用**。

相比于 jQuery，axios 更加**轻量化**，只专注于网络数据请求。

## **6.2 axios** **发起** **GET** **请求**

```
 axios.get('url', { params: { /*参数*/ } }).then(callback)
```

```
 // 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/get'
 // 请求的参数对象
 var paramsObj = { name: 'zs', age: 20 }
 // 调用 axios.get() 发起 GET 请求
 axios.get(url, { params: paramsObj }).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(res)
 })
```

## **6.3 axios** **发起** **POST** **请求**

```
 axios.post('url', { /*参数*/ }).then(callback)
```

```
 // 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/post'
 // 要提交到服务器的数据
 var dataObj = { location: '北京', address: '顺义' }
 // 调用 axios.post() 发起 POST 请求
 axios.post(url, dataObj).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(result)
 })
```

## **6.4** **直接使用** **axios** **发起请求**

axios 也提供了类似于 jQuery 中 $.ajax() 的函数，语法如下：

```
 axios({
     method: '请求类型',
     url: '请求的URL地址',
     data: { /* POST数据 */ },
     params: { /* GET参数 */ }
 }) .then(callback)
```

**1.** **直接使用** **axios** **发起** **GET** **请求**

```
   
 axios({
     method: 'GET',
     url: 'http://www.liulongbin.top:3006/api/get',
     params: { // GET 参数要通过 params 属性提供
         name: 'zs',
         age: 20
     }
 }).then(function(res) {
     console.log(res.data)
 })
```

**2.** **直接使用** **axios** **发起** **POST** **请求**

```
   
 axios({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/post',
     data: { // POST 数据要通过 data 属性提供
         bookname: '程序员的自我修养',
         price: 666
     }
 }).then(function(res) {
     console.log(res.data)
 })
```

