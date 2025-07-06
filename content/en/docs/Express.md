---
title: Express
slug: Express
lastmod: 2025-07-01T00:00:00+00:00
---

# Express

CSDN [https://blog.csdn.net/weixin_44070254/article/details/118480069](https://blog.csdn.net/weixin_44070254/article/details/118480069)

javascript 标准 [http://javascript.ruanyifeng.com/nodejs/express.html#toc3](http://javascript.ruanyifeng.com/nodejs/express.html#toc3)

官网 [https://www.expressjs.com.cn/starter/hello-world.html](https://www.expressjs.com.cn/starter/hello-world.html)

# 1. 概述

Express 是目前最流行的基于 Node.js 的 Web 开发框架，可以快速地搭建一个完整功能的网站

Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法，使用Express 开发框架可以非常方便、快速的创建 Web 网站的服务器或 [API](https://so.csdn.net/so/search?q=API&spm=1001.2101.3001.7020) 接口的服务器

# 2. Hello World

**下载 express**

Express上手非常简单，首先新建一个项目目录，假定叫做hello-world

通过 `npm init`  命令为你的应用新建一个package.json文件

```jsx
{
  "name": "hello-world",
  "description": "hello world test app",
  "version": "0.0.1",
  "private": true,
  "dependencies": {
    "express": "4.x"
  }
}
```

然后执行

```jsx
npm install
或者 npm install express --save
```

**使用 get 方法**

在项目根目录下，新建一个启动文件，假定叫做server.js

```jsx
var express = require('express');
var app = express();
app.listen(3000); // 监听 3000 端口
```

启动脚本index.js的`app.get`方法，用于指定不同的访问路径所对应的回调函数，这叫做“路由”（routing）

```jsx
// server.js 

var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello world!');
});
app.get('/customer', function(req, res){
  res.send('customer page');
});
app.get('/admin', function(req, res){
  res.send('admin page');
});

app.listen(3000);
```

**路由封装：**

最好就把路由放到一个单独的文件中，比如新建一个 routes 子目录

```jsx
// routes/server.js

module.exports = function (app) {
  app.get('/', function (req, res) {
    res.send('Hello world');
  });
  app.get('/customer', function(req, res){
    res.send('customer page');
  });
  app.get('/admin', function(req, res){
    res.send('admin page');
  });
};
```

原来的index.js就变成下面这样

```jsx
// server.js

var express = require('express');
var app = express();
var routes = require('./routes')(app);
app.listen(3000);
```

# 3. **运行原理**

## http 模块

Express框架建立在node.js内置的http模块上，Express框架的核心是对http模块的再包装

http模块生成服务器的原始代码如下：

```jsx
var http = require("http");

var app = http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello world!");
});

app.listen(3000, "localhost");
```

上面代码的关键是http模块的createServer方法，表示生成一个HTTP服务器实例。该方法接受一个回调函数，该回调函数的参数，分别为代表HTTP请求和HTTP回应的request对象和response对象

上面的代码用Express改写如下：

```jsx
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello world!');
});

app.listen(3000);
```

原来是用`http.createServer`方法新建一个app实例，现在则是用Express的构造方法，生成一个Epress实例。两者的回调函数都是相同的。Express框架等于在http模块之上，加了一个中间层。

## 中间件 middleware

中间件（middleware）就是处理 HTTP 请求的函数。它最大的特点就是，一个中间件处理完，再传递给下一个中间件。App 实例在运行过程中，会调用一系列的中间件

每个中间件可以从 App 实例，接收三个参数，依次为request对象（HTTP请求）、response对象（HTTP回应），next回调函数（下一个中间件）。每个中间件都可以对HTTP请求（request对象）进行加工，并且决定是否调用 next 方法，将 request 对象再传给下一个中间件

一个不进行任何操作、只传递 request 对象的中间件，就是下面这样

```jsx
function uselessMiddleware(req, res, next) {
  next();
}
```

上面代码的next就是下一个中间件。如果它带有参数，则代表抛出一个错误，参数为错误文本

```jsx
function uselessMiddleware(req, res, next) {
  next('出错了！');
}
```

## app.use 方法

use是express注册中间件的方法，它返回一个函数

1. 下面是一个连续调用两个中间件的例子
    
    ```jsx
    var express = require("express");
    var http = require("http");
    
    var app = express();
    
    app.use(function(request, response, next) {
      console.log("In comes a " + request.method + " to " + request.url);
      next();
    });
    
    app.use(function(request, response) {
      response.writeHead(200, { "Content-Type": "text/plain" });
      response.end("Hello world!\n");
    });
    
    http.createServer(app).listen(1337);
    ```
    
    上面代码使用`app.use`方法，注册了两个中间件。收到HTTP请求后，先调用第一个中间件，在控制台输出一行信息，然后通过`next`方法，将执行权传给第二个中间件，输出HTTP回应。由于第二个中间件没有调用`next`方法，所以request对象就不再向后传递了
    

1. `use`方法内部可以对访问路径进行判断，据此就能实现简单的路由，根据不同的请求网址，返回不同的网页内容
    
    ```jsx
    var express = require("express");
    var http = require("http");
    
    var app = express();
    
    app.use(function(request, response, next) {
      if (request.url == "/") {
        response.writeHead(200, { "Content-Type": "text/plain" });
        response.end("Welcome to the homepage!\n");
      } else {
        next();
      }
    });
    
    app.use(function(request, response, next) {
      if (request.url == "/about") {
        response.writeHead(200, { "Content-Type": "text/plain" });
      } else {
        next();
      }
    });
    
    app.use(function(request, response) {
      response.writeHead(404, { "Content-Type": "text/plain" });
      response.end("404 error!\n");
    });
    
    http.createServer(app).listen(1337);
    ```
    
    上面代码通过`request.url`属性，判断请求的网址，从而返回不同的内容。注意，`app.use`方法一共登记了三个中间件，只要请求路径匹配，就不会将执行权交给下一个中间件。因此，最后一个中间件会返回404错误，即前面的中间件都没匹配请求路径，找不到所要请求的资源
    
2. 除了在回调函数内部判断请求的网址，use方法也允许将请求网址写在第一个参数。这代表，只有请求路径匹配这个参数，后面的中间件才会生效
    
    ```jsx
    app.use('/path', someMiddleware);
    ```
    
    上面的代码可以写成下面的样子
    
    ```jsx
    var express = require("express");
    var http = require("http");
    
    var app = express();
    
    app.use("/home", function(request, response, next) {
      response.writeHead(200, { "Content-Type": "text/plain" });
      response.end("Welcome to the homepage!\n");
    });
    
    app.use("/about", function(request, response, next) {
      response.writeHead(200, { "Content-Type": "text/plain" });
      response.end("Welcome to the about page!\n");
    });
    
    app.use(function(request, response) {
      response.writeHead(404, { "Content-Type": "text/plain" });
      response.end("404 error!\n");
    });
    
    http.createServer(app).listen(1337);
    ```
    
3. 设置静态文件目录
    
    ```jsx
    // 设定静态文件目录，比如本地文件
    // 目录为demo/public/images，访问
    // 网址则显示为http://localhost:3000/images
    app.use(express.static(path.join(__dirname, 'public')));
    ```
    

# 4. Express 方法

针对不同的请求，Express提供了use方法的一些别名

## **get**

上面的功能代码可以改写为：

```jsx
var express = require("express");
var http = require("http");
var app = express();

app.all("*", function(request, response, next) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  next();
});

app.get("/", function(request, response) {
  response.end("Welcome to the homepage!");
});

app.get("/about", function(request, response) {
  response.end("Welcome to the about page!");
});

app.get("*", function(request, response) {
  response.end("404!");
});

http.createServer(app).listen(1337);
```

上面代码的all方法表示，所有请求都必须通过该中间件，参数中的“*”表示对所有路径有效。get方法则是只有GET动词的HTTP请求通过该中间件，它的第一个参数是请求的路径。由于get方法的回调函数没有调用next方法，所以只要有一个中间件被调用了，后面的中间件就不会再被调用了

## **post/put/delete**

除了get方法以外，Express还提供post、put、delete方法，即HTTP动词都是Express的方法

get - 查询请求 - 条件在地址栏

post - 新增请求 - 数据在请求主体

put - 修改请求 - 条件在地址栏 - 数据在请求主体

delete - 删除请求 - 条件在地址栏

## **set**

set方法用于指定变量的值

```jsx
// 设定port变量，意为访问端口
app.set('port', process.env.PORT || 3000);
// 设定views变量，意为视图存放的目录
app.set("views", path.join(__dirname, 'views'));
// 设定view engine变量，意为网页模板引擎
app.set("view engine", "jade");
```

**模式匹配**

这些方法的第一个参数，都是请求的路径。除了绝对匹配以外，Express允许模式匹配

```jsx
app.get("/hello/:who", function(req, res) {
  res.end("Hello, " + req.params.who + ".");
});
```

上面代码将匹配“/hello/alice”网址，网址中的alice将被捕获，作为req.params.who属性的值

## response

```jsx
res.download() // 提示下载文件。	
res.end() // 终结响应处理流程。
res.json() // 发送一个 JSON 格式的响应。
res.jsonp() // 发送一个支持 JSONP 的 JSON 格式的响应。
res.redirect() // 重定向请求。
res.render() // 渲染视图模板。
res.send() // 发送各种类型的响应。
res.sendFile() // 以八位字节流的形式发送文件。
res.sendStatus() // 设置响应状态代码，并将其以字符串形式作为响应体的一部分发送。
```

response.redirect方法允许网址的重定向

```jsx
response.redirect("/hello/anime");
response.redirect("http://www.example.com");
response.redirect(301, "http://www.example.com");
```

response.sendFile方法用于发送文件

```jsx
response.sendFile("/path/to/anime.mp4");
```

response.render方法用于渲染网页模板

下面代码使用render方法，将message变量传入index模板，渲染成HTML网页

```jsx
app.get("/", function(request, response) {
  response.render("index", { message: "Hello World" });
});
```

response.json 给客户端响应json数据

```jsx

// res.json(json格式的数据)
let obj = {
    name:"张三",
    age:12,
    wife:"翠花",
    children:['阿大','阿二','小明']
}
res.json(obj)
```

res.send() 用于给客户端响应字符串的，字符串中如果是标签，可解析成html，自动设置数据类型和编码

```jsx
// res.send()
let html = `<h2>这是一个h2标签</h2>`
// res.end 不会自动设置数据类型，也不会设置编码
// res.end(html)
res.send(html)
```

## request

```jsx
req.url // 请求的路径 - 如果有?传参，这个路径中也会带有参数
req.method // 请求方法
req.path // 请求路径 - 如果有?传参，这个路径中不包含参数
req.protocol // 协议
req.params // 获取get请求的参数 - 针对动态路由传参 - restful风格的参数 - 最终获取到的是对象，对象的键，就是路径指定的名称
req.query // 获取get请求的参数 - 针对传统形式传参 - 使用?参数 - 最终获取到的是对象
request.ip // 用于获得HTTP请求的IP地址
request.files // 用于获取上传的文件
```